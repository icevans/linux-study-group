# Redirection, Pipeline, and Standard Stream Questions

1. List the contents of both `/bin` and `/sbin`, and write the output to a file called `system_binaries.txt` -- do this all with a single shell command. (Hint: you will need to use file globbing, aka wildcards.)

1. Perform the same command as the previous exercise, but this time, use a Unix pipeline to number the list before sending it to `system_binaries.txt` -- again, this should all be a single command. (Hint: `man nl`)

1. Create the same list as in exercise #1, but instead of redirecting the output to a file, pipe it to a utility that will output a filtered list that includes only those items that contain the string 'grep' in their name. (Hint: `man grep`)

1. The previous exercise revealed several different `grep` utilities. If you want to try your hand at regular expressions, and a bit of review from unit one's reading, use `egrep` (or `grep -E`) to create a list of only those versions of grep that are _not_ links to other `greps`. (Hint: you'll probably want to start by generating a list using the long listing format: `man ls`)

1. Find out how many commands are saved in your shell history, but do not rely on a full printing-to-screen of the history list. You'll probably want to start the pipeline with `history`. If you aren't familiar with the history library, enter `history` to see its output and/or check out `man history`. (Hint: `wc` may be helpful; you could also try it by restricting the output of `history` and piping that into a utility that outputs only one of the columns.)

1. List only the first two users (first alphabetically) with accounts on your system. You can find a list of users (sorted by userid) at `/etc/passwd`. (Hint: `man head`)

1. Make a small file directly at the command line using `cat` with no arguments. The first line of your small file should just contain your first name; the rest of the lines are up to you. Then use `grep` to list all the lines in your small file that *do not* contain your first name.

1. Enter a command that you know will fail (ex: `$ ls kjfksdfjlskfjl`) and redirect the standard output to the bitbucket (`/dev/null`). You should still see an error message printed to your terminal. Now rerun the failing command and this time redirect the standard error to the bitbucket. Finally, rerun your failing command and redirect both stdout and stderr to the bitbucket with a single command.

1. List all of the users who have logged in to your server. A useful command for this is ​`lastlog​`. Make sure you only list users that have actually logged in.

1. List all of the members in the Linux study group that you created in the exercises in Unit 1. You can find a list of groups at ​`/etc/group​`. Bonus: see if you can print out just the user names of the group members with one command (you should have access to this command if you are running Ubuntu on a Digital Ocean droplet).

1. Using one command, write the entire contents of /bin to a file named `bin.txt`, then output a filtered list that contains the string 'grub'. (hint: `man tee`)

1. For the following exercise(s), clone the following repository, which contains empty text files named after animals: `https://github.com/ridergit/linux-practice-files`
Using two utilities, count the number of files named after animals that end with either 'nk', 'ck', or 'ek' (eg: 'skunk.txt'). There should be five!
