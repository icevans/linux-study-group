1. What does `chmod 755` accomplish? Rewrite the same thing using symbolic notation.
    `chmod 755` sets the permission of the file owner, the members of the file's group, and world to read and execute. It also make it so that it is only writable by the file's owner. This can be represented in symbolic notation as `chmod a=rw,u+x`
    
2. When a user creates a new file or directory, who owns it? Verify this using the `sudo` command to create a file as another user on your system. (Note: this command is normally used to run commands as the root user, but can actually be used to run a command as any user on the system. Consult the man page to figure out how to do this.)
   When a user creates file, it is the user who owns it. I tried the verification step of using the `sudo` command to create a file as another user and this resulted in a permission denied response.
   
    Here are the results for creating a file as me:
    ```terminal
    $ touch victor_file
    $ ls -la
    drwxrwxr-x 2 victor victor 4096 Nov  4 03:47 .
    drwxr-xr-x 6 victor victor 4096 Nov  4 03:46 ..
    -rw-rw-r-- 1 victor victor    0 Nov  4 03:47 victor_file  # I'm the owner
    ```
   
    Here are the results for creating a file as another user (ice):
    ```terminal
    $ sudo -u ice touch ice_file
    [sudo] password for victor:
    touch: cannot touch 'ice_file': Permission denied
    $ sudo -l
    User victor may run the following commands on ubuntu-ls-linux-study-group:
    (ALL : ALL) ALL
    ```
    
    Going by the results, I think the permission denied is for the creating of the file as the user "ice". I think this is the case because going by the command that I can run as `sudo` (via checking `sudo -l`), I should be allowed to use ALL commands as ALL users and as ALL commnads. (note: `sudo` -l` list the commands you can use as `sudoer`; [this digitalocean article](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file-on-ubuntu-and-centos) gives an idea of how to interpret the result). To test out my idea, I'll go back to this agin after exercise 4 (creating of shared directory)
        
3. Create a group called, say, `linux_study` for all the linux study group members you created (if you didn't create any, creat some accounts now, but no need to worry about setting up SSH keys and all that jazz -- you just need multiple user accounts to work with). Add yourself and all the users you created to this group. (This exercise and the next closely follow the books example of creating a shared music directory.)

    ```terminal
    $ sudo groupadd linux_study
    [sudo] password for victor:
    $ sudo usermod -a -G linux_study ice
    # ... repeat for all users you want to add
    $ grep linux_study /etc/group
    linux_study:x:1009:ice,jvt,dana,andy_h,benh,jstryer,charles,catherine
    ```
    
    For this exercise, I leaned on google for instructions. This [article I found](https://www.techrepublic.com/article/how-to-create-users-and-groups-in-linux-from-the-command-line/) was good enough to accomplish the exercise requirement.

3. Create a directory where this group can share documents with each other called, say, `linux_group_docs`. `/usr/local/share` is a reasonable place to put this.
   - The directory will need appropriate group ownership and permissions so that users in the `linux_study` group can add files to it.
   - When a user adds a file to this directory, other users from the group (but no one else) should be able to edit it.
   - If a user creates a subdirectory to edit files, other users should be able view the contents of this subdirectory and add files to it.
   - Verify this all works using the sudo command as in exercise 2.
   



1. What does the executable permission mean for a directory?
    The executable permission for a directory allows the creating, deleting, and renaming of files within it.
