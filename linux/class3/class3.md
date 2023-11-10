## Linux Command use flow
##### Bellow shows some Linux commands with a description.

### View a file one page at a time using `less/more`
21. Use `less`

```
$ less class3.md
```
- Use the arrow keys or the `j` and `k` keys to scroll up and down.
- To move forward one page, press the Spacebar or the Page Down key.
- To move back one page, press `b` or the Page Up key.
- To quit less, press the `q` key.
- Search text within the file by pressing `'/',` the insert `text` press `enter`. 

22. Use `more`

```
$ more class3.md
```
- `more` is similar to `less` but has `less` functionality


#### `less` is more versatile and allows you to scroll in both directions, search for text, and provides a more interactive experience

### Display the beginning or end of a file- `head/tail`

`head` and `tail` are command-line utilities used to display the beginning (head) and end (tail) of text files, respectively. They are commonly used to view a portion of a file, often for the purpose of previewing its contents or monitoring log files.

23. Use `head`
```
$ head class3.md
```
- By default, `head` displays the first 10 lines.
```
$ head -n 20 class3.md
```
- This displays the first 20 lines of `class3.md` using `-n`.

24. Use `tail`

To view the end of a file, you can use the `tail` command in a similar manner to `head`. By default, `tail` displays the last 10 lines of a file

```
$ tail class3.md

$ tail -n 20 class3.md

$ tail -f logfile
```
- If you want to continuously monitor a file, such as a log file, you can use the `-f` option.

#### Text editors for creating and editing files- `nano/vi`

25. nano/vi Use

```
$ nano filename
$ vi filename
```
#### Use `grap` (Search for text in files.)

It seems like you meant to refer to the grep command, which is a powerful tool for searching and manipulating text in Linux and Unix-like operating systems. grep allows you to search for specific text patterns within files or the output of other commands.

26. Use `grap` default

```
$ grep 'monitor' class3.md
```
- This will show full sentences with bold searching(`monitor`) words.

```
$ grep -n 'monitor' class3.md
```
- This will show the lines containing "monitor" along with their corresponding line numbers.

```
$ grep -n -A 1 -B 2 'monitor' class3.md
```
- `-n` will show line number
- `-A` 1 will show 1 line after the matching line.
- `-B` 2 will show 2 lines before the matching line.

```
$ grep -n '.*searching.*' class3.md
```
- This will show you all lines in the file that contain the word `searching`.

