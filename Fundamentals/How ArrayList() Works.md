`ArrayList` has the basic data structure:

```java
private transient Object[] elementData;
```

When we actually create an `ArrayList` the following piece of code is executed:

```java
 this.elementData = new Object[initial capacity];
```

`ArrayList` can be created in the two ways mentioned below:

1. `List list = new ArrayList();`

The default constructor is invoked and will internally create an array of `Object` with default size 10.

2. `List list = new ArrayList(5);`

When we create an `ArrayList` in this way, constructor with an integer argument is invoked and create an array of `Object` with default size 5.

Inside the `add` method there is check whether the current size of filled elements is greater/equal to the maximum size of the `ArrayList` then it will create new `ArrayList` with the size new `arraylist = (current arraylist*3/2)+1` and copy the data from old to new array list.