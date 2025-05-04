**Introduction**

Working with Excel documents is a frequently used feature in a software application.

In this article, a way to generalize the writing to an Excel file for any type of Objects with both single and composite(array) types of fields has been achieved using Apache POI with the support of Java Reflection feature. The need for custom code for writing each type of fields and row-column processing has been reduced, you are good to go with minimum customization.

Apache POI (Poor Obfuscation Implementation) is a popular open source library run by the Apache Software Foundation which is developed for reading and writing files in Microsoft Office formats, such as Word, PowerPoint, and Excel.

The objective of [Apache POI](https://javarevisited.blogspot.com/2015/06/how-to-read-write-excel-file-java-poi-example.html) is to design a cross-platform API that can manipulate various file formats of Microsoft Office and Open Office Documents. Since we are focusing on writing Excel files, we will be using the following file formats of Apache POI for spreadsheets.

> HSSF (Horrible Spreadsheet Format) − It is used for xlsx file format of MS-Excel (97–2007) files.
> 
> XSSF (XML Spreadsheet Format) − It is used for xlsx file format of MS-Excel (2007 and later) files.

Each of the Apache POI libraries are dedicated to manipulate each particular type of file. The XSSF library contains the classes for handling the xlsx Excel format. The figure below shows the Apache POI related interfaces and classes for manipulating xlsx Excel files.

[

![](https://miro.medium.com/v2/resize:fit:726/1*7n-ep8DljW5yAhbB5PZXMw.png)

](https://www.java67.com/2014/09/how-to-read-write-xlsx-file-in-java-apache-poi-example.html)

Furthermore it provides excellent support for additional excel features such as working with Formulas, creating cell styles by filling colors and borders, fonts, headers and footers, data validations, images, hyperlinks etc.

Lets dive in to the work.

These main steps will be followed for the implementation :

1. _Setting up a Spring Boot project with Apache POI dependencies and other necessary dependencies._
2. _Creating an API endpoint to send an HTTP request to download the Excel file._
3. _==Defining the Java Annotation interfaces which will be used for the dynamic class reflection.==_
4. _Defining the Java POJO class which will be used to write into the Excel sheet. And s_etting up a POJO class to hold metadata for each field of the above class.
5. _Implementing the generic Xlsx writer with dynamic class reflection and POI spreadsheet data population into the workbook._
6. _Fetching the list of POJO class objects and passing to the writer and get the response as an byte array._
7. _Sending API response as a data byte array with relevant header details of openxmlformats as the MediaType_

**Setting up a Spring Boot project with Apache POI dependencies and other necessary dependencies**

<dependency>  
   <groupId>org.apache.poi</groupId>  
   <artifactId>poi</artifactId>  
   <version>4.1.2</version>  
</dependency>  
<dependency>  
   <groupId>org.apache.poi</groupId>  
   <artifactId>poi-ooxml</artifactId>  
   <version>4.1.2</version>  
</dependency>

**Creating an API endpoint to receive a HTTP request to download the Excel file**

```java
@RequestMapping(method = RequestMethod._POST_, value = "/download-users-excel")  
public ResponseEntity downloadUsersExcel() {  
    try {  
        final byte[] data = userService.getUserXlsData();  
        HttpHeaders header = new HttpHeaders();  
    header.setContentType(MediaType._parseMediaType_("application/vnd.openxmlformats-officedocument.spreadsheetml.sheet;charset=UTF-8"));  
        header.set(HttpHeaders._CONTENT_DISPOSITION_, "inline; filename= users.xlsx");  
        header.setContentLength(data.length);  
        return new ResponseEntity<>(data, header, HttpStatus._OK_);  
    } catch (Exception e) {  
        return new ResponseEntity<>(null, HttpStatus._INTERNAL_SERVER_ERROR_);  
    }  
}

```
**Defining the Java Annotation interfaces which will be used for the dynamic class reflection**

```java
@Documented  
@Target(ElementType._TYPE_)  
@Retention(RetentionPolicy._RUNTIME_)  
public @interface XlsxSheet {  
    String value();  
}@Documented  
@Target(ElementType._FIELD_)  
@Retention(RetentionPolicy._RUNTIME_)  
public @interface XlsxSingleField {  
    int columnIndex();  
}@Documented  
@Target(ElementType._FIELD_)  
@Retention(RetentionPolicy._RUNTIME_)  
public @interface XlsxCompositeField {  
    int from();  
    int to();  
}

```
**Defining the Java POJO class which will be used to write into the Excel sheet**

Here for the demonstration purpose, a POJO which includes User details with a list of DietPlan is used :

```java
@Getter  
@NoArgsConstructor  
@AllArgsConstructor  
@Setter  
@XlsxSheet(value = "Users")  
public class XlsxUser {  
  
    @XlsxSingleField(columnIndex = 0)  
    private String name;  
    @XlsxSingleField(columnIndex = 1)  
    private String gender;  
    @XlsxSingleField(columnIndex = 2)  
    private Integer age;  
    @XlsxSingleField(columnIndex = 3)  
    private Double bmiValue;  
    @XlsxSingleField(columnIndex = 4)  
    private Boolean isOverweight;  
    @XlsxSingleField(columnIndex = 5)  
    private List<String> activities;  
    @XlsxCompositeField(from = 6, to = 7)  
    private List<XlsxDietPlan> plans;  
  
    @Getter  
    @AllArgsConstructor  
    @NoArgsConstructor  
    @Setter  
    public static class XlsxDietPlan {  
        @XlsxSingleField(columnIndex = 6)  
        private String mealName;  
        @XlsxSingleField(columnIndex = 7)  
        private Double calories;  
    }  
  
}
```

As shown above, the previously defined Annotations are used to provide metadata for the POJO class and its fields. This metadata will be evaluated at runtime for the POJO class reflection and populating the workbook in the generic writer.

**Setting up a POJO class to hold metadata for each field of the above class**

If we observe it, the possible dataset class might most probably consist of following data structures.

1. Single fields (Integer, String, Float, Double, Boolean types)
2. Array fields (List of single fields)
3. Composite fields (List of objects that consists of single fields)

So each field is mapped to a XlsxField instance which holds metadata about the POJO class field which will be useful later.

```java
@Getter  
@NoArgsConstructor  
@AllArgsConstructor  
@Setter  
public class XlsxField {  
    private String fieldName;  
    private int cellIndex;  
    private int cellIndexFrom;  
    private int cellIndexTo;  
    private boolean isAnArray;  
    private boolean isComposite;  
}
```

**Implementing the generic Xlsx writer with dynamic class reflection and POI spreadsheet data population into workbook**

```java
@Service  
public class XlsxFileWriter  {  
  
  
   private static final Logger _logger_ = LoggerFactory._getLogger_(XlsxFileWriter.class);  
  
    public <T> void write(List<T> data, ByteArrayOutputStream bos, String[] columnTitles, Workbook workbook) {  
  
        if (data.isEmpty()) {  
            _logger_.error("No data received to write Xls file..");  
            return;  
        }  
  
        long start = System._currentTimeMillis_();  
  
//      setting up the basic styles for the workbook  
        Font boldFont = getBoldFont(workbook);  
        Font genericFont = getGenericFont(workbook);  
        CellStyle headerStyle = getLeftAlignedCellStyle(workbook, boldFont);  
        CellStyle currencyStyle = setCurrencyCellStyle(workbook);  
        CellStyle centerAlignedStyle = getCenterAlignedCellStyle(workbook);  
        CellStyle genericStyle = getLeftAlignedCellStyle(workbook, genericFont);  
  
   try {  
// using POJO class metadata for the sheet name  
    XlsxSheet annotation = data.get(0).getClass().getAnnotation(XlsxSheet.class);  
    String sheetName = annotation.value();  
    Sheet sheet = workbook.createSheet(sheetName);  
  
//  get the metadata for each field of the POJO class into a list  
    List<XlsxField> xlsColumnFields = _getFieldNamesForClass_(data.get(0).getClass());  
  
      int tempRowNo = 0;  
      int recordBeginRowNo = 0;  
      int recordEndRowNo = 0;  
  
//    set spreadsheet titles  
      Row mainRow = sheet.createRow(tempRowNo);  
      Cell columnTitleCell;  
  
      for (int i = 0; i < columnTitles.length; i++) {  
        columnTitleCell = mainRow.createCell(i);  
        columnTitleCell.setCellStyle(headerStyle);  
        columnTitleCell.setCellValue(columnTitles[i]);  
      }  
      recordEndRowNo++;  
  
//    get class of the passed dataset  
      Class<?> clazz = data.get(0).getClass();//    looping the past dataset  
      for (T record : data) {  
        tempRowNo = recordEndRowNo;  
        recordBeginRowNo = tempRowNo;  
        mainRow = sheet.createRow(tempRowNo++);  
        boolean isFirstValue;  
        boolean isFirstRow;  
        boolean isRowNoToDecrease = false;  
        Method xlsMethod;  
        Object xlsObjValue;  
        ArrayList<Object> objValueList;  
                  
//      get max size of the record if its multiple row  
        int maxListSize = getMaxListSize(record, xlsColumnFields, clazz);  
                  
                  
//      looping through the fields of the current record  
        for (XlsxField xlsColumnField : xlsColumnFields) {  
//       writing a single field  
         if (!xlsColumnField.isAnArray() && !xlsColumnField.isComposite()) {  
            writeSingleFieldRow(mainRow, xlsColumnField, clazz, currencyStyle, centerAlignedStyle, genericStyle,  
                                record, workbook);  
  
//       overlooking the next field and adjusting the starting row  
         if (isNextColumnAnArray(xlsColumnFields, xlsColumnField, clazz, record)) {  
             isRowNoToDecrease = true;  
             tempRowNo = recordBeginRowNo + 1;  
          }  
  
//       writing an single array field  
         } else if (xlsColumnField.isAnArray() && !xlsColumnField.isComposite()) {  
           xlsMethod = getMethod(clazz, xlsColumnField);  
           xlsObjValue = xlsMethod.invoke(record, (Object[]) null);  
           objValueList = (ArrayList<Object>) xlsObjValue;  
           isFirstValue = true;  
  
//       looping through the items of the single array  
         for (Object objectValue : objValueList) {  
            Row childRow;  
            if (isFirstValue) {  
             childRow = mainRow;  
             writeArrayFieldRow(childRow, xlsColumnField, objectValue, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
             isFirstValue = false;  
            } else if (isRowNoToDecrease) {  
             childRow = getOrCreateNextRow(sheet, tempRowNo++);  
             writeArrayFieldRow(childRow, xlsColumnField, objectValue, currencyStyle, centerAlignedStyle,genericStyle, workbook);  
             isRowNoToDecrease = false;  
            } else {  
             childRow = getOrCreateNextRow(sheet, tempRowNo++);  
             writeArrayFieldRow(childRow, xlsColumnField, objectValue, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
            }  
          }  
  
 //      overlooking the next field and adjusting the starting row  
         if (isNextColumnAnArray(xlsColumnFields, xlsColumnField, clazz, record)) {  
            isRowNoToDecrease = true;  
            tempRowNo = recordBeginRowNo + 1;  
         }  
  
//      writing a composite array field  
         } else if (xlsColumnField.isAnArray() && xlsColumnField.isComposite()) {  
           xlsMethod = getMethod(clazz, xlsColumnField);  
           xlsObjValue = xlsMethod.invoke(record, (Object[]) null);  
           objValueList = (ArrayList<Object>) xlsObjValue;  
           isFirstRow = true;  
  
//       looping through the items of the composite array  
           for (Object objectValue : objValueList) {  
             Row childRow;  
             List<XlsxField> xlsCompositeColumnFields = _getFieldNamesForClass_(objectValue.getClass());  
             if (isFirstRow) {  
               childRow = mainRow;  
               for (XlsxField xlsCompositeColumnField : xlsCompositeColumnFields) {    
                                                                  writeCompositeFieldRow(objectValue, xlsCompositeColumnField, childRow, currencyStyle,centerAlignedStyle, genericStyle, workbook);  
               }  
              isFirstRow = false;  
              } else if (isRowNoToDecrease) {  
               childRow = getOrCreateNextRow(sheet, tempRowNo++);  
               for (XlsxField xlsCompositeColumnField : xlsCompositeColumnFields) {  
                                    writeCompositeFieldRow(objectValue, xlsCompositeColumnField, childRow, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
            }  
            isRowNoToDecrease = false;  
           } else {  
            childRow = getOrCreateNextRow(sheet, tempRowNo++);  
            for (XlsxField xlsCompositeColumnField : xlsCompositeColumnFields) {  
                                    writeCompositeFieldRow(objectValue, xlsCompositeColumnField, childRow, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
           }  
          }  
         }  
  
//       overlooking the next field and adjusting the starting row  
         if (isNextColumnAnArray(xlsColumnFields, xlsColumnField, clazz, record)) {  
            isRowNoToDecrease = true;  
            tempRowNo = recordBeginRowNo + 1;  
           }  
         }  
       }  
  
//      adjusting the ending row number for the current record  
        recordEndRowNo = maxListSize + recordBeginRowNo;  
     }  
  
// auto sizing the columns of the whole sheet  
   autoSizeColumns(sheet, xlsColumnFields.size());              
   workbook.write(bos);  
   _logger_.info("Xls file generated in [{}] seconds", processTime(start));  
  } catch (Exception e) {  
    _logger_.info("Xls file write failed", e);  
  }  
}  
```


```java
  
  private void writeCompositeFieldRow(Object objectValue, XlsxField xlsCompositeColumnField, Row childRow,CellStyle currencyStyle, CellStyle centerAlignedStyle, CellStyle genericStyle, Workbook workbook) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {  
  
        Method nestedCompositeXlsMethod = getMethod(objectValue.getClass(), xlsCompositeColumnField);  
        Object nestedCompositeValue = nestedCompositeXlsMethod.invoke(objectValue, (Object[]) null);  
        Cell compositeNewCell = childRow.createCell(xlsCompositeColumnField.getCellIndex());  
        setCellValue(compositeNewCell, nestedCompositeValue, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
    }  
  
    private void writeArrayFieldRow(Row childRow, XlsxField xlsColumnField, Object objectValue,  
                                    CellStyle currencyStyle, CellStyle centerAlignedStyle, CellStyle genericStyle, Workbook workbook) {  
        Cell newCell = childRow.createCell(xlsColumnField.getCellIndex());  
        setCellValue(newCell, objectValue, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
    }  
  
    private <T> void writeSingleFieldRow(Row mainRow, XlsxField xlsColumnField, Class<?> clazz, CellStyle currencyStyle,CellStyle centerAlignedStyle, CellStyle genericStyle, T record, Workbook workbook) throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {  
  
  Cell newCell = mainRow.createCell(xlsColumnField.getCellIndex());  
  Method xlsMethod = getMethod(clazz, xlsColumnField);  
  Object xlsObjValue = xlsMethod.invoke(record, (Object[]) null);  
  setCellValue(newCell, xlsObjValue, currencyStyle, centerAlignedStyle, genericStyle, workbook);  
    }  
  
    private <T> boolean isNextColumnAnArray(List<XlsxField> xlsColumnFields, XlsxField xlsColumnField,Class<?> clazz, T record)  
            throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {  
  XlsxField nextXlsColumnField;  
  int fieldsSize = xlsColumnFields.size();  
  Method nestedXlsMethod;  
  Object nestedObjValue;  
  ArrayList<Object> nestedObjValueList;  
   if (xlsColumnFields.indexOf(xlsColumnField) < (fieldsSize - 1)) {  
      nextXlsColumnField = xlsColumnFields.get(xlsColumnFields.indexOf(xlsColumnField) + 1);  
  if (nextXlsColumnField.isAnArray()) {  
   nestedXlsMethod = getMethod(clazz, nextXlsColumnField);  
   nestedObjValue = nestedXlsMethod.invoke(record, (Object[]) null);  
   nestedObjValueList = (ArrayList<Object>) nestedObjValue;  
                return nestedObjValueList.size() > 1;  
            }  
        }  
        return xlsColumnFields.indexOf(xlsColumnField) == (fieldsSize - 1);  
  
    }  
  
    private void setCellValue(Cell cell, Object objValue, CellStyle currencyStyle, CellStyle centerAlignedStyle,  
                              CellStyle genericStyle, Workbook workbook) {  
        Hyperlink link = workbook.getCreationHelper().createHyperlink(HyperlinkType._URL_);  
          if (objValue != null) {  
            if (objValue instanceof String) {  
                String cellValue = (String) objValue;  
                cell.setCellStyle(genericStyle);  
                if (cellValue.contains("https://") || cellValue.contains("http://")) {  
                    link.setAddress(cellValue);  
                    cell.setCellValue(cellValue);  
                    cell.setHyperlink(link);  
                } else {  
                    cell.setCellValue(cellValue);  
                }  
            } else if (objValue instanceof Long) {  
                cell.setCellValue((Long) objValue);  
            } else if (objValue instanceof Integer) {  
                cell.setCellValue((Integer) objValue);  
            } else if (objValue instanceof Double) {  
                Double cellValue = (Double) objValue;  
                cell.setCellStyle(currencyStyle);  
                cell.setCellValue(cellValue);  
            } else if (objValue instanceof Boolean) {  
                cell.setCellStyle(centerAlignedStyle);  
                if (objValue.equals(true)) {  
                    cell.setCellValue(1);  
                } else {  
                    cell.setCellValue(0);  
                }  
            }  
        }  
    }  
  
    private static List<XlsxField> getFieldNamesForClass(Class<?> clazz) {  
        List<XlsxField> xlsColumnFields = new ArrayList();  
        Field[] fields = clazz.getDeclaredFields();  
        for (Field field : fields) {  
          XlsxField xlsColumnField = new XlsxField();  
           if (Collection.class.isAssignableFrom(field.getType())) {  
                xlsColumnField.setAnArray(true);  
                XlsxCompositeField xlsCompositeField = field.getAnnotation(XlsxCompositeField.class);  
                if (xlsCompositeField != null) {  
          xlsColumnField.setCellIndexFrom(xlsCompositeField.from());  
              xlsColumnField.setCellIndexTo(xlsCompositeField.to());  
                    xlsColumnField.setComposite(true);  
                } else {  
                    XlsxSingleField xlsField = field.getAnnotation(XlsxSingleField.class);  
                xlsColumnField.setCellIndex(xlsField.columnIndex());  
                }  
            } else {  
                XlsxSingleField xlsField = field.getAnnotation(XlsxSingleField.class);  
                xlsColumnField.setAnArray(false);  
                if (xlsField != null) {  
                xlsColumnField.setCellIndex(xlsField.columnIndex());  
                    xlsColumnField.setComposite(false);  
                }  
            }  
            xlsColumnField.setFieldName(field.getName());  
            xlsColumnFields.add(xlsColumnField);  
        }  
        return xlsColumnFields;  
    }  
  
    private static String capitalize(String s) {  
        if (s.length() == 0)  
            return s;  
        return s.substring(0, 1).toUpperCase() + s.substring(1);  
    }  
  
  
    private <T> int getMaxListSize(T record, List<XlsxField> xlsColumnFields, Class<? extends Object> aClass)  
            throws NoSuchMethodException, InvocationTargetException, IllegalAccessException {  
  
        List<Integer> listSizes = new ArrayList<>();  
        for (XlsxField xlsColumnField : xlsColumnFields) {  
          if (xlsColumnField.isAnArray()) {  
           Method method = getMethod(aClass, xlsColumnField);  
            Object value = method.invoke(record, (Object[]) null);  
             ArrayList<Object> objects = (ArrayList<Object>) value;  
                if (objects.size() > 1) {  
                  listSizes.add(objects.size());  
                }  
            }  
        }  
  
        if (listSizes.isEmpty()) {  
            return 1;  
        } else {  
            return Collections._max_(listSizes);  
        }  
  
    }  
  
    private Method getMethod(Class<?> clazz, XlsxField xlsColumnField) throws NoSuchMethodException {  
        Method method;  
        try {  
            method = clazz.getMethod("get" + _capitalize_(xlsColumnField.getFieldName()));  
        } catch (NoSuchMethodException nme) {  
            method = clazz.getMethod(xlsColumnField.getFieldName());  
        }  
  
        return method;  
    }  
  
    private long processTime(long start) {  
        return (System._currentTimeMillis_() - start) / 1000;  
    }  
  
    private void autoSizeColumns(Sheet sheet, int noOfColumns) {  
        for (int i = 0; i < noOfColumns; i++) {  
            sheet.autoSizeColumn((short) i);  
        }  
    }  
  
    private Row getOrCreateNextRow(Sheet sheet, int rowNo) {  
        Row row;  
        if (sheet.getRow(rowNo) != null) {  
            row = sheet.getRow(rowNo);  
        } else {  
            row = sheet.createRow(rowNo);  
        }  
        return row;  
    }  
  
    private CellStyle setCurrencyCellStyle(Workbook workbook) {  
        CellStyle currencyStyle = workbook.createCellStyle();  
        currencyStyle.setWrapText(true);  
        DataFormat df = workbook.createDataFormat();  
        currencyStyle.setDataFormat(df.getFormat("#0.00"));  
        return currencyStyle;  
    }  
  
    private Font getBoldFont(Workbook workbook) {  
        Font font = workbook.createFont();  
        font.setBold(true);  
        font.setFontHeight((short) (10 * 20));  
        font.setFontName("Calibri");  
        font.setColor(IndexedColors._BLACK_.getIndex());  
        return font;  
    }  
  
    private Font getGenericFont(Workbook workbook) {  
        Font font = workbook.createFont();  
        font.setFontHeight((short) (10 * 20));  
        font.setFontName("Calibri");  
        font.setColor(IndexedColors._BLACK_.getIndex());  
        return font;  
    }  
  
    private CellStyle getCenterAlignedCellStyle(Workbook workbook) {  
        CellStyle cellStyle = workbook.createCellStyle();  
        cellStyle.setAlignment(HorizontalAlignment._CENTER_);  
        cellStyle.setVerticalAlignment(VerticalAlignment._BOTTOM_);  
        cellStyle.setBorderTop(BorderStyle._NONE_);  
        cellStyle.setBorderBottom(BorderStyle._NONE_);  
        cellStyle.setBorderLeft(BorderStyle._NONE_);  
        cellStyle.setBorderRight(BorderStyle._NONE_);  
        return cellStyle;  
    }  
  
    private CellStyle getLeftAlignedCellStyle(Workbook workbook, Font font) {  
        CellStyle cellStyle = workbook.createCellStyle();  
        cellStyle.setFont(font);  
        cellStyle.setAlignment(HorizontalAlignment._LEFT_);  
        cellStyle.setVerticalAlignment(VerticalAlignment._BOTTOM_);  
        cellStyle.setBorderTop(BorderStyle._NONE_);  
        cellStyle.setBorderBottom(BorderStyle._NONE_);  
        cellStyle.setBorderLeft(BorderStyle._NONE_);  
        cellStyle.setBorderRight(BorderStyle._NONE_);  
        return cellStyle;  
    }  
}

```
**Fetching the list of POJO class objects and passing to the writer and get the response as a** [**byte array**](https://javarevisited.blogspot.com/2020/04/7-examples-to-read-file-into-byte-array-in-java.html)

For the demonstration purpose, some dummy data will be used to create the sample POJO records list.

Then an instances of [ByteArrayOutputStream](https://javarevisited.blogspot.com/2014/04/how-to-convert-byte-array-to-inputstream-outputstream-java-example.html) and XSSFWorkbook are created. The titles of the spreadsheet are defined as an String array. These are passed to the writer as parameters. The passed instance of ByteArrayOutputStream is contained the byte stream of the data written into the workbook. Inside the Finally clause the ByteArrayOutputStream is closed and the byte array is returned.

```java
@Service  
public class UserServiceImpl implements UserService {  
  
    private final XlsxWriter xlsxWriter;  
    private static final Logger _logger_ = LoggerFactory._getLogger_(UserServiceImpl.class);  
  
    public UserServiceImpl(XlsxWriter xlsxWriter) {  
        this.xlsxWriter = xlsxWriter;  
    }  
  
    @Override  
    public byte[] getUserXlsData() throws IOException {  
        List<XlsxUser> xlsxUserList = new ArrayList<>();  
        for (int i = 0; i < 10; i++) {  
            XlsxUser user = new XlsxUser();  
            List<String> activities = new ArrayList<>(Arrays._asList_("Running", "Working out", "Heavy Machinery", "Walking"));  
            List<XlsxUser.XlsxDietPlan> plans = new ArrayList<>(Arrays._asList_(new XlsxUser.XlsxDietPlan("Breakfast", 500.10),  
                    new XlsxUser.XlsxDietPlan("Lunch", 320.25), new XlsxUser.XlsxDietPlan("Dinner", 200.80)));  
            user.setName("John Doe");  
            user.setAge(25);  
            user.setBmiValue(25.36);  
            user.setGender("Male");  
            user.setIsOverweight(true);  
            user.setActivities(activities);  
            user.setPlans(plans);  
            xlsxUserList.add(user);  
        }  
        ByteArrayOutputStream bos = new ByteArrayOutputStream();  
        try (Workbook workbook = new XSSFWorkbook()) {  
            String[] columnTitles = new String[]{"Name", "Gender", "Age", "BMI value", "Is Overweight", "Activities", "Meal Name", "Calories"};  
            xlsxWriter.write(xlsxUserList, bos, columnTitles, workbook);  
        } catch (Exception e) {  
            _logger_.error("Generating users xls file failed", e);  
        } finally {  
            bos.close();  
        }  
        return bos.toByteArray();  
     }  
}

```
## Sample Output

[

![](https://miro.medium.com/v2/resize:fit:1400/1*r_BfykDo6CO9llGyrI-Jfw.png)

](https://javarevisited.blogspot.com/2020/11/top-10-business-and-finance-courses.html#axzz6v6xLSPvq)

**Summary**

An effort to implement a generic and robust Excel writer using Apache POI and Java core features such as Reflection and Annotations, which will download an Excel file using an HTTP request. This would match most of the use cases of POJO structures when its written to an Excel sheet. Hope this will help and will be easy to customize as well.

The repository for the project can be found in [here](https://github.com/jsb9009/generic-xlsx-writer).

Feel free to leave a comment below. Hope you enjoyed the story..! :)