原文地址：https://www.tecmint.com/sed-add-a-line-after-string-in-file/





# How to Append a Line After a String in a File Using sed Command



If you’re working with text files on a Linux system, you may need to modify the contents of those files. One useful tool for this task is [sed](https://www.tecmint.com/linux-sed-command-tips-tricks/), which stands for **stream editor**, which allows you to perform various text manipulations, such as replacing text, deleting lines, and adding new lines.

In this article, we’ll show you how to use `sed` to add a new line after a specific string in a file.

## What is sed?

`sed` is a command-line tool used for text processing, which reads input line by line, applies the specified operation, and then outputs the result.

You can use `sed` to perform tasks like:

- Searching and replacing text
- Inserting or deleting lines
- Modifying text based on patterns

In our case, we will use `sed` to add a line after a particular string in a file.

## How to Add a Line After a String in a File



Let’s say you have a file called `example.txt` with the following content:

```
Hello, this is a test file.
This is the second line.
We are learning how to use sed.
This is the last line.
```

Now, suppose you want to add a new line after the string “**learning how to use sed**“, you can use the following `sed` command syntax.

```
sed '/pattern/a\new line of text' filename
```

Let’s break down this command:

- `/pattern/` is the search pattern that tells **sed** to look for a specific string in the file and replace pattern with the string you’re searching for.
- `a\` is the append command that tells **sed** to add a new line after the line containing the search pattern.
- `new line of text` is the text you want to add.
- `filename` is the name of the file you want to modify.

Let’s say we want to add the line “`This is the new line!`” after the string “`learning how to use sed`” in the file `example.txt`.

```
sed '/learning how to use sed/a\This is the new line!' example.txt
```

This will print the content of the file with the new line added after the matched string as shown.

```
Hello, this is a test file.
This is the second line.
We are learning how to use sed.
This is the new line!
This is the last line.
```

However, this command only shows the output on the terminal and does not change the file itself.

If you want to save the changes directly to the file, you can use the `-i` option with `sed` to edit the file in place.

```
sed -i '/learning how to use sed/a\This is the new line!' example.txt
```



After running this command, the file `example.txt` will be updated with the new line added.

##### Conclusion

Using `sed` to add a line after a string in a file is simple and powerful. You can easily modify files without needing to open them in a text editor. This method is particularly useful when you want to automate text file modifications or make changes to large files quickly.

Remember:

- Use `/pattern/a\new line` to add a line after a specific string.
- Use `-i` to save changes directly to the file.

With this knowledge, you can start editing files more efficiently using `sed`!
