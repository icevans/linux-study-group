# Shell Expansion, Quoting, and Keyboard Tricks Exercises Solutions

1. Using brace expansion, make a directory of .txt files that holds files following the pattern: [a-c][1-3][a-c].txt (E.g. a1a.txt, a1b.txt, a1c.txt ... c3a.txt, c3b.txt, c3c.txt). Then, remove all the files where the middle number is 3. 

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
