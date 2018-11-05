1. What does `chmod 755` accomplish? Rewrite the same thing using symbolic notation.

    `chmod 755` sets the permission of the file owner, the members of the file's group, and world to read and execute. It also make it so that it is only writable by the file's owner. This can be represented in symbolic notation as `chmod a=rx,u+w`
    
2. When a user creates a new file or directory, who owns it? Verify this using the `sudo` command to create a file as another user on your system. (Note: this command is normally used to run commands as the root user, but can actually be used to run a command as any user on the system. Consult the man page to figure out how to do this.)

    When a user creates file, it is the user who owns it. I tried the verification step of using the `sudo` command to create a file as another user and this resulted in a permission denied response.
   
    Here are the results for creating a file as me:
    ```terminal
    $ touch victor_file
    $ ls -la
    drwxrwxr-x 2 victor victor 4096 Nov  4 03:47 .            // permissions for directory
    drwxr-xr-x 6 victor victor 4096 Nov  4 03:46 ..
    -rw-rw-r-- 1 victor victor    0 Nov  4 03:47 victor_file  // I'm the owner
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
    
    Going by the results, I think the permission denied is for the creating of the file as the user "ice". I think this is the case because going by the command that I can run as `sudo` (via checking `sudo -l`), I should be allowed to use ALL commands as ALL users and as ALL commnads. (note: `sudo -l` list the commands you can use as `sudoer`; [this digitalocean article](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file-on-ubuntu-and-centos) gives an idea of how to interpret the result). Also, based on the permissions of the directory only `victor` and user of the `victor` group have write permissions. To test out my idea, I'll go back to this agin after exercise 4 (creating of shared directory)
        
3. Create a group called, say, `linux_study` for all the linux study group members you created (if you didn't create any, creat some accounts now, but no need to worry about setting up SSH keys and all that jazz -- you just need multiple user accounts to work with). Add yourself and all the users you created to this group. (This exercise and the next closely follow the books example of creating a shared music directory.)

    For this exercise, I leaned on google for instructions. This [article I found](https://www.techrepublic.com/article/how-to-create-users-and-groups-in-linux-from-the-command-line/) was good enough to accomplish the exercise requirement.

    ```terminal
    $ sudo groupadd linux_study
    [sudo] password for victor:
    $ sudo usermod -a -G linux_study ice
    // ... repeat for all users you want to add
    $ grep linux_study /etc/group
    linux_study:x:1009:ice,jvt,dana,andy_h,benh,jstryer,charles,catherine,victor
    ```

4. Create a directory where this group can share documents with each other called, say, `linux_group_docs`. `/usr/local/share` is a reasonable place to put this.
    - The directory will need appropriate group ownership and permissions so that users in the `linux_study` group can add files to it.
    - When a user adds a file to this directory, other users from the group (but no one else) should be able to edit it.
    - If a user creates a subdirectory to edit files, other users should be able view the contents of this subdirectory and add files to it.
    - Verify this all works using the sudo command as in exercise 2.
   
    ```terminal
    // create shared directory
    $ cd /usr/local/share
    $ sudo mkdir linux_group_docs
    [sudo] password for victor:
    $ cd linux_group_docs
    $ ls -ld
    drwxr-xr-x 2 root root 4096 Nov  4 05:58 .
    // change group ownership and permissions
    $ sudo chown :linux_study /usr/local/share/linux_group_docs
    $ sudo chmod 775 .
    $ ls -ld
    drwxrwxr-x 2 root linux_study 4096 Nov  4 05:58 .
    // the linux_group_docs is now owned by the linux_study group
    // members of the linux_study group have read, write, and execute permissions
    ```
    
    Given the above directory, I tried working on exercise 2 again but this time using the shared directory.
    
    ```terminal
    // Note: You may need to log in and out for the permission to take effect
    $ pwd
    /usr/local/share/linux_group_docs
    $ touch victor_file
    $ sudo -u ice touch ice_file
    [sudo] password for victor:
    $ ls -la
    -rw-r--r-- 1 ice    ice            0 Nov  4 06:20 ice_file
    -rw-rw-r-- 1 victor victor         0 Nov  4 06:17 victor_file
    ```
    
    Based on the result, I think this verifies my answer that the owner of the creator of the file is the user.
    
    For bullets two (2) and three (3), I think the permission will be dependent on the default `umask` for each user that created the file or directory. As such, I decided not to puruse implementing those anymore. Chapter 9 of TLCL has a solution but it only lasts until the end of a session.

5. Who is allowed to create, rename, or delete files in the shared directory?

   Those who are allowed create, rename, or delete files are those with "write" permissions granted that the "execute" attribute is also set. In the case of the shared directory, root and members of linux_study can create, rename, or delete files in the shared directory.

   ```terminal
   // permissions for linux_group_docs
   drwxrwxr-x 2 root   linux_study 4096 Nov  4 06:30 .
   ```

6. What does the executable permission mean for a directory?
    The executable permission for a directory allows the entering of the directory.
    
7. What permissions does the `irb` file have? (Hint: you'll have to find where `irb` lives using the info from chapter 3. It may be a symbolic link on your system -- TLCL discusses permissions for symbolic links.)

    Note: It looks like ruby is not installed by default (at least from my virtual machine).
    
    Based on the information form chapter 3 it should be in `/usr/bin` since _"it contains the executable programs installed by your Linux distribution. It is not uncommon for this directory to hold thousands of programs."_. 
    
    That said, I did the following commands to find the answer for this question.
    
    ```terminal
    $ ls -la /usr/bin/irb
    lrwxrwxrwx 1 root root 8 Feb 15  2014 /usr/bin/irb -> irb1.9.1
    // return value shows that `irb` is a symbolic link to irb1.9.1 in the current directory
    $ ls -la /usr/bin/irb1.9.1
    -rwxr-xr-x 1 root root 319 Jun  8 17:06 /usr/bin/irb1.9.1
    // permission is 755; root, members of root, and world have read and execute permissions
    // only root has write permission.
    ```
    
8. Change the permissions on `irb` to 754. Does the fact that it's a symbolic link change how you go about doing this? What does this do? What impact does it have on your ability to use `irb`? Put back the correct permissions.

    The fact that it's a symbolic link doesn't impact if perform chmod on it.
    
    ```terminal
    $ sudo chmod 754 /usr/bin/irb
    $ ls -la /usr/bin/irb
    lrwxrwxrwx 1 root root 8 Feb 15  2014 /usr/bin/irb -> irb1.9.1
    // recall that All symbolic links have “dummy” permissions.
    $ ls -la /usr/bin/irb1.9.1
    -rwxr-xr-- 1 root root 319 Jun  8 17:06 /usr/bin/irb1.9.1
    // the execute permission is removed from "world"
    ```
    
    Changing the permission to 754 prevents me (victor) from using the `irb` command since only root and members of root can execute it. 
    
9. DON'T DO THE FOLLOWING, IT'S JUST A THOUGHT EXPERIMENT: What would happen if you changed the owner and group of the `sudo` command to your own user accont?
    
    I was initially thinking nothing bad will happen since the "world" will have execute permission. It turns out `sudo` must be run as the root user. I don't completely understand this one but the gist is that changing the owner of `sudo` to other than `root` breaks the command. There are lots of horror stories I came across when searching for the impact of changing the owner of `sudo` to other than `root`. I'll probably only explore this again if I get into learning about security, I think.
    
    

