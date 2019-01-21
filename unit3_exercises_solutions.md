# Shell Expansion, Quoting, and Keyboard Tricks Exercises Solutions

1. Use brace expansion to create a series of directories, running from `dir001` to `dir100`. Ensure the numerical portion of each directory has the appropriate amount of leading zeros.

  - `mkdir dir{001..100}`

1. As above, use brace expansion to create a series of directories with leading zeros from `skip001` to `skip100`, but this time only every 4th number should result in a directory. For example, the first three directories in the series will be `skip001`, `skip005`, and `skip009`. The final directory will be `skip097`.

  - `mkdir skip{001..100..4}`

1. Use brace expansion to print the following to stdout: `test01{01..03} test02{01..03} test03{01..03}`. Hint: How can we _suppress_ expansion?

  - `echo test{01..03}\{01..03\}`
  - or: `echo test{01..03}'{01..03}'`

1. Enter `env` to print a list of environmental variables. Identify a few that interest you and practice parameter expansion by echoing their values to stdout.
  - e.g. `echo ${SHELL}` for the path to your current shell's executable.
  - e.g. `echo ${OLDPWD}` for the previous working directory.

1. Review `grep` and the just-used `env` by using these two commands to retrieve the same variables/values you played with in the previous exercise.

  - e.g. `env | grep '^SHELL'` for the path to your current shell's executable.
  - e.g. `env | grep '^OLDPWD'` for the previous working directory.

1. Use command substitution to provide the directory argument in a call to `ls -l`.  For example, say you wanted the details for the directory that houses your `ruby` command, but you don't know the path to that directory, or just as likely, you can't remember whether you are using the system `ruby` or `rbenv`'s.Find the information with a command of the following form: `ls -l <command substitution magic here>`. Hint: `man which`.

  - `ls -l $(which ruby)`

1. Using brace expansion, make a directory of .txt files that holds files following the pattern: [a-c][1-3][a-c].txt (E.g. a1a.txt, a1b.txt, a1c.txt ... c3a.txt, c3b.txt, c3c.txt). Then, remove all files where the middle number is 3. 

    - solution to create files: 
    ```  
    mkdir Files
    cd Files
    touch {a..c}{1..3}{a..c}.txt
    ```
  
    - solution to remove files with 3 as the middle character: 
    ```
    rm {a..c}3{a..c}.txt
    ```
  
2. Using parameter expansion, print to console the current working directory that you are in. (Hint: echo)
    - solution: 
    ```
    echo "${PWD##*/}"
    ```
