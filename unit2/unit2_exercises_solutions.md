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
    - or even: `ls -lh /bin /sbin | grep 'grep$' | grep -v '^l'`

1. Find out how many commands are saved in your shell history, but do not rely on a full printing-to-screen of the history list. You'll probably want to start the pipeline with `history`. If you aren't familiar with the history library, enter `history` to see its output and/or check out `man history`. (Hint: `wc` may be helpful; you could also try it by restricting the output of `history` and piping that into a utility that outputs only one of the columns.)

    - solution: `history | wc -l`
    - also: `history | tail -n 1 | awk '{print $1}'`
    - or even: `history | tail -n 1 | cut -d ' ' -f 3`
      - this last one is a bit of a hack; you'll need to see if your shell outputs the history list with spaces as left padding, and pick the correct 'field' accordingly

1. List only the first two users (first alphabetically) with accounts on your system. You can find a list of users (sorted by userid) at `/etc/passwd`. (Hint: `man head`)

    - solution: `cat /etc/passwd | sort | head -n 2`

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
    # or simply: 
    grep -v 'Kurth' grepTest
   ```

1. Enter a command that you know will fail (ex: `$ ls kjfksdfjlskfjl`) and redirect the standard output to the bitbucket (`/dev/null`). You should still see an error message printed to your terminal. Now rerun the failing command and this time redirect the standard error to the bitbucket. Finally, rerun your failing command and redirect both stdout and stderr to the bitbucket with a single command.

    - solution:
    ```bash
    ls foo > /dev/null
    ls foo 2> /dev/null
    ls foo &> /dev/null
   ```

1. List all of the users who have logged in to your server. A useful command for this is ​`lastlog​`. Make sure you only list users that have actually logged in.

    - solution: `lastlog | grep -v '**Never logged in**'`
    - or: `lastlog | grep -v "**Never logged in**"`

        - Note that including multiple words in the pattern will require either single or double quotes to suppress shell's word splitting/argument parsing. Without the quotes the shell will send each word following `-v` to `grep` as a separate argument, so it will only search for the first as a pattern and regard the other two words as arguments referencing the files in which to search.

1. List all of the members in the Linux study group that you created in the exercises in Unit 1. You can find a list of groups at ​`/etc/group​`. Bonus: see if you can print out just the user names of the group members with one command (you should have access to this command if you are running Ubuntu on a Digital Ocean droplet).

    - solution: `cat /etc/group | grep '^linux_study_group' | cut -d ':' -f 4`
    - piped to `sed` for better formatting: `cat /etc/group | grep '^linux_study_group' | cut -d ':' -f 4 | sed 's/,/, /g'`

    - Bonus solution: `sudo groupmems -g linux_study_group -l`

1. Using one command, write the entire contents of /bin to a file named `bin.txt`, then output a filtered list that contains the string 'grub'. (hint: `man tee`)

    - solution: `ls /bin | tee bin.txt | grep 'grub'`

1. For the following exercise(s), clone the following repository, which contains empty text files named after animals: `https://github.com/ridergit/linux-practice-files`
Using two utilities, count the number of files named after animals that end with either 'nk', 'ck', or 'ek' (eg: 'skunk.txt'). There should be five!

     - solution: `grep -E '[nce]k\.txt$' linux-practice-files-master/* | wc -l`

1. Working with the same directory (as problem 12), sort files by time created and output the top 10 to a file.

    - solution: `ls -lt linux-practice-files | head > a_sorted_file.txt`
1. Sort files by time created, output it to a file, then print the top 10 onto the terminal in long form.

    - solution: `ls -lt linux-practice-files > a_sorted_file.txt | head`

1. Count the number of files that exists in the directory, and count the number of lines that is the file, make sure they are the same (and they should be, as long as you have not manipulated the output).
    
    - solution: `ls  ~/linux-practice-files/ | wc -l` counts the number of files in the directory
    - `wc -l a_sorted_file.txt` counts the number of lines in the outputted file

1. If you came up with the following solution, `ls -t linux-practice-files |head | tee a_sorted_file.txt` for the problem above, count the number of lines in the outputted file versus the solution using the > operator. Is this the same number as the solution using the > operator ? What causes the disprepancy?

    - solution: This is the result of pipe failing due to the `| head` at the end. As soon as `head` finds and displays 10 lines of text, the previous processes will get killed. In the 2nd case, `head` never gets any input, so it doesn't terminate the pipe process early. 
        - Note that this is not the case with `tail`.
