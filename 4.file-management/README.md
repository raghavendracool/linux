# File management in Linux

### File and Directory Management
1. **`ls`** – Lists files and directories in the current location.
2. **`cd /path/to/directory`** – Changes the working directory.
3. **`pwd`** – Prints the current working directory.
4. **`mkdir new_folder`** – Creates a new directory.
5. **`rmdir empty_folder`** – Removes an empty directory.
6. **`rm file.txt`** – Deletes a file.
7. **`rm -r folder`** – Deletes a folder and its contents.
8. **`cp file1.txt file2.txt`** – Copies a file.
9. **`cp -r dir1 dir2`** – Copies a directory recursively.
10. **`mv old_name new_name`** – Moves or renames a file or directory.

### File Viewing and Editing
11. **`cat file.txt`** – Displays file content.
12. **`tac file.txt`** – Displays file content in reverse order.
13. **`less file.txt`** – Opens a file for viewing with scrolling support.
14. **`more file.txt`** – Similar to `less`, but only moves forward.
15. **`head -n 10 file.txt`** – Displays the first 10 lines of a file.
16. **`tail -n 10 file.txt`** – Displays the last 10 lines of a file.
17. **`nano file.txt`** – Opens a simple text editor.
18. **`vi file.txt`** – Opens a powerful text editor.
19. **`echo 'Hello' > file.txt`** – Writes text to a file, overwriting existing content.
20. **`echo 'Hello' >> file.txt`** – Appends text to a file without overwriting.

| Command             | Use                                   |
| ------------------- | ------------------------------------- |
| `ls`                | List files and folders                |
| `ls -a`             | Show hidden files also                |
| `ls -l`             | Show detailed list                    |
| `ls -lh`            | Detailed list with readable size      |
| `ls -lt`            | Latest modified file first            |
| `ls -ltr`           | Oldest first, latest at bottom        |
| `ls -lrth`          | Oldest first, readable size, detailed |
| `ls -larth`         | Same as above + hidden files          |
| `ls -R`             | Show files inside subdirectories also |
| `ls -d */`          | Show only directories                 |
| `ls *.log`          | Show only `.log` files                |
| `ls -lhS`           | Sort by file size, biggest first      |
| `ls -lSrh`          | Sort by file size, smallest first     |
| `ls -i`             | Show inode number                     |
| `ls -ld foldername` | Show folder details, not inside files |

