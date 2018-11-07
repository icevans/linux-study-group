# Redirection, Pipeline, and Standard Stream Questions

1. List the contents of both `/bin` and `/sbin`, and write the output to a file called `system_binaries.txt` -- do this all with a single shell command. (Hint: you will need to use file globbing, aka wildcards.)

2. Perform the same command as the previous exercise, but this time, use a Unix pipeline to number the list before sending it to `system_binaries.txt` -- again, this should all be a single command. (Hint: `man nl`)

3. Find out how many commands are saved in your shell history, but do not rely on a full printing-to-screen of the history list. You'll probably want to start the pipeline with `history`. If you aren't familiar with the history library, enter `history` to see its output and/or check out `man history`. (Hint: `wc` may be helpful; you could also try it by restricting the output of `history` and piping that into a utility that outputs only one of the columns.)
