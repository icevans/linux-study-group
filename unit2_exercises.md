# Redirection, Pipeline, and Standard Stream Questions

1. List the contents of both `/bin` and `/sbin`, and write the output to a file called `system_binaries.txt` -- do this all with a single shell command. (Hint: you will need to use file globbing, aka wildcards.)

2. Perform the same command as the previous exercise, but this time, use a Unix pipeline to number the list before sending it to `system_binaries.txt` -- again, this should all be a single command. (Hint: `man nl`)