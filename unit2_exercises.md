# Redirection, Pipeline, and Standard Stream Questions

1. List the contents of both `/bin` and `/sbin`, and write the output to a file called `system_binaries.txt` -- do this all with a single shell command. (Hint: you will need to use file globbing, aka wildcards.)

    - solution: `ls /bin /sbin > system_binaries.txt`

1. Perform the same command as the previous exercise, but this time, use a Unix pipeline to number the list before sending it to `system_binaries.txt` -- again, this should all be a single command. (Hint: `man nl`)

    - solution: `ls -lah /bin /sbin | nl > system_binaries_numbered.txt`

1. Create the same list as in exercise #1, but instead of redirecting the output to a file, pipe it to a utility that will output a filtered list that includes only those items that contain the string 'grep' in their name. (Hint: `man grep`)

    - solution: `ls /bin /sbin | grep 'grep'`

1. The previous exercise revealed several different `grep` utilities. If you want to try your hand at regular expressions, and a bit of review from unit one's reading, use `egrep` (or `grep -E`) to create a list of only those versions of grep that are _not_ links to other `greps`. (Hint: you'll probably want to start by generating a list using the long listing format: `man ls`)

    - solution: `ls -lh /bin /sbin | grep -E '^[^l].+grep$'`
    - also: `ls -lh /bin /sbin | grep -E '^-.+grep$'`

1. Find out how many commands are saved in your shell history, but do not rely on a full printing-to-screen of the history list. You'll probably want to start the pipeline with `history`. If you aren't familiar with the history library, enter `history` to see its output and/or check out `man history`. (Hint: `wc` may be helpful; you could also try it by restricting the output of `history` and piping that into a utility that outputs only one of the columns.)

    - solution: `history | wc -l`
    - also: `history | tail -1 | awk '{print $1}'`
    - or even: `history | tail -1 | cut -d ' ' -f 3`
      - this last one is a bit of a hack; you'll need to see if your shell outputs the history list with spaces as left padding, and pick the correct 'field' accordingly

1. List only the first two users (first alphabetically) with accounts on your system. You can find a list of users (sorted by userid) at `/etc/passwd`. (Hint: `man head`)

    - solution: `cat /etc/passwd | sort | head -2`

1. Make a small file directly at the command line using `cat` with no arguments. The first line of your small file should just contain your first name; the rest of the lines are up to you. Then use `grep` to list all the lines in your small file that *do not* contain your first name.

    - solution:
    ```bash
    # create file
    $ cat > grepTest
    Kurth
    some words by Kurth
    more words
    Kurth
    even more input
    Ha!  # type `Ctl+d` to send typed chars to the program currently reading from the terminal

    # `grep` for lines _not_ containing first name
    cat grepTest | grep -v 'Kurth'
   ```

1. Enter a command that you know will fail (ex: `$ ls kjfksdfjlskfjl`) and redirect the standard output to the bitbucket (`/dev/null`). You should still see an error message printed to your terminal. Now rerun the failing command and this time redirect the standard error to the bitbucket. Finally, rerun your failing command and redirect both stdout and stderr to the bitbucket with a single command.

    - solution:
    ```bash
    ls foo > /dev/null
    ls foo 2> /dev/null
    ls foo &> /dev/null
   ```

1. List all of the users who have logged in to your server. A useful command for this is ​`lastlog​`. Make sure you only list users that have actually logged in.

1. List all of the members in the Linux study group that you created in the exercises in Unit 1. You can find a list of groups at ​`/etc/group​`. Bonus: see if you can print out just the user names of the group members with one command (you should have access to this command if you are running Ubuntu on a Digital Ocean droplet).

