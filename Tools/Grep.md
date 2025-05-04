In its simplest form, `grep` takes a piece of text followed by one or more filenames and prints all of the lines in those files that contain that text.

`grep` can search for patterns as well; we will explore those in the next course. What's more important right now is some of `grep`'s more common flags:

- `-c`: print a count of matching lines rather than the lines themselves
- `-i`: ignore case (e.g., treat "Regression" and "regression" as matches)
- `-n`: print line numbers for matching lines

- `-h`: do _not_ print the names of files when searching multiple files
- `-l`: print the names of files that contain matches, not the matches
- `-v`: invert the match, i.e., only show lines that _don't_ match
- `-r`: for Recursive Search
- `-A1`:will output the matched line and the line after it.
- `-B1`:will output the matched line and the line before it.
- `-C1`:for One line Before and After including Matched line.
Combining Multiple Commands with Grep
```bash
cut -d , -f 2 seasonal/summer.csv | grep -v Tooth
```
> Wildcard with Grep

The shell has other wildcards as well, though they are less commonly used:

- `?` matches a single character, so `201?.txt` will match `2017.txt` or `2018.txt`, but not `2017-01.txt`.
- `[...]` matches any one of the characters inside the square brackets, so `201[78].txt` matches `2017.txt` or `2018.txt`, but not `2016.txt`.
- `{...}` matches any of the comma-separated patterns inside the curly brackets, so `{*.txt, *.csv}` matches any file whose name ends with `.txt` or `.csv`, but not files whose names end with `.pdf`.


> Sorting
- `sort` puts data in order. By default it does this in ascending alphabetical order, but the flags 
	- `-n` and `-r` can be used to sort numerically and reverse the order of its output,
	- `-b` tells it to ignore leading blanks 
	- `-f` tells it to **f**old case (i.e., be case-insensitive)
	- `-n` for longest value

> Finding Unique using `uniq` command

- ` uniq` 

> 

```bash
wc -l $@ | grep -v total | sort -n -r | head -n 1
```

Finding any file in Use

```bash
sudo fs_usage | grep my.cnf
```
