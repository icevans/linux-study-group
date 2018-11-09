# Redirection, Pipeline, and Standard Stream Questions

1. List the contents of both `/bin` and `/sbin`, and write the output to a file called `system_binaries.txt` -- do this all with a single shell command. (Hint: you will need to use file globbing, aka wildcards.)

2. Perform the same command as the previous exercise, but this time, use a Unix pipeline to number the list before sending it to `system_binaries.txt` -- again, this should all be a single command. (Hint: `man nl`)

3. Make a small file directly at the command line using `cat` with no arguments. The first line of your small file should just contain your first name; the rest of the lines are up to you. Then use `grep` to list all the lines in your small file that *do not* contain your first name.

4. Enter a command that you know will fail (ex: `$ ls kjfksdfjlskfjl`) and redirect the standard output to the bitbucket (`/dev/null`). You should still see an error message printed to your terminal. Now rerun the failing command and this time redirect the standard error to the bitbucket. Finally, rerun your failing command and redirect both stdout and stderr to the bitbucket with a single command.

