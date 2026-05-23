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

# File Management in Linux

### Common `ls` Commands for Daily Use

1. **`ls`** – Lists files and directories in the current location.
2. **`ls -a`** – Shows all files, including hidden files.
3. **`ls -l`** – Shows files and directories in detailed long-list format.
4. **`ls -lh`** – Shows detailed list with file sizes in human-readable format like KB, MB, GB.
5. **`ls -lt`** – Lists files by modified time, latest file first.
6. **`ls -ltr`** – Lists files by modified time in reverse order, oldest first and latest at bottom.
7. **`ls -lrth`** – Shows detailed list with human-readable size, oldest first and latest file at bottom.
8. **`ls -larth`** – Same as `ls -lrth`, but also shows hidden files.
9. **`ls -R`** – Lists files and directories recursively, including subdirectories.
10. **`ls -d */`** – Shows only directories in the current location.
11. **`ls *.log`** – Lists only files ending with `.log`.
12. **`ls -lhS`** – Lists files by size, biggest file first.
13. **`ls -lSrh`** – Lists files by size in reverse order, smallest file first.
14. **`ls -i`** – Shows inode number of files and directories.
15. **`ls -ld foldername`** – Shows details of a directory itself, not the files inside it.

### Most Used `ls` Commands in Real Time

16. **`ls -lrth /var/log/`** – Checks latest log files, with the newest file at the bottom.
17. **`ls -larth ~`** – Shows all files, including hidden files, in the home directory.
18. **`ls -lhS`** – Checks the biggest files in the current directory.
19. **`ls -d */`** – Shows only directories.
20. **`ls -ld /var/www/html`** – Checks folder permissions and ownership.
21. **`ls -lrth *.log`** – Shows all `.log` files with the latest log file at the bottom.

### Easy Notes

- **`ls -lrth`** = Latest file at the bottom.
- **`ls -larth`** = Latest file at the bottom + hidden files also.
- **`ls -lhS`** = Biggest file at the top.
- **`ls -ld foldername`** = Check directory permission.
