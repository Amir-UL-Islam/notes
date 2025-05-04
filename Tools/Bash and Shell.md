> cat

You can use `cat` to print large files and then scroll through the output.

`cut -f 2-5,8 -d , values.csv`
Which means "select columns 2 through 5 and columns 8, using comma as the separator". cut uses -f (meaning "fields") to specify columns and -d (meaning "delimiter") to specify the separator. You need to specify the latter because some files may use spaces, tabs, or colons to separate columns.

> cut 

> What can't cut do?

`cut` is a simple-minded command. In particular, **it doesn't understand quoted strings**. 

If, for example, your file is: Name,Age "Johel,Ranjit",28 "Sharma,Rupinder",26 then:
`cut -f 2 -d everyone.csv` -> will produce: Age Ranjit"Rupinder"

> less

One page is displayed at a time. You can press spacebar to page down or type `q` to quit.

> `head` and `tail` let you select rows from a text file.

> head
- `-n` will print `n` number of lines 
> Use `tail` with the flag `-n +7` to display all _but_ the first six lines of `seasonal/spring.csv`.

> Loops in Bash

```bash
for filetype in gif jpg png; do echo $filetype; done
```

```bash
for filename in $@
do
cut -d , -f 1 $filename | grep -v Date | sort | head -n 1
cut -d , -f 1 $filename | grep -v Date | sort | tail -n 1
done
```
1. The structure is `for` …variable… `in` …list… `; do` …body… `; done`
2. The list of things the loop is to process (in our case, the words `gif`, `jpg`, and `png`).
3. The variable that keeps track of which thing the loop is currently processing (in our case, `filetype`).
4. The body of the loop that does the processing (in our case, `echo $filetype`).
> You have to Use `;`Semi-colons in order  to separate the Commands
```bash
for filename in *.csv; do echo "From file" $filename; head -n 6 $filename | tail -n 5 ; done
```

> Input Parameters
- `$@`For Input Parameter
- Shell lets you use `$1`, `$2`, and so on to refer to specific command-line parameters.
```bash
cut -d , -f $2 $1
```

```bash
head -n 5 | tail -n 3 somefile.txt
```
then `tail` goes ahead and prints the last three lines of `somefile.txt`, but `head` waits forever for keyboard input, since it wasn't given a filename and there isn't anything ahead of it in the pipeline.

> ARGV
