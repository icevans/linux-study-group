# Permissions Practice

Below are some exercises you can use to practice setting and managing permissions on your Linux system. Remember that all processes run as users, so the user of a process needs the right permissions to all files it may need to access. A web server also runs as a user, and it's not root (why not?) So, if you're trying to host a website and you set the wrong permissions for the site directory... broken website. But, of course, devs might also need access to these files. These sorts of issues are why permissions matter to web developers.

The book contains most of the information you need for this, but you should consult command man pages liberally -- it's good to get used to reading these. `man sudo` contains lots of interesting information, for example.

1. What does `chmod 755` accomplish? Rewrite the same thing using symbolic notation.
1. When a user creates a new file or directory, who owns it? Verify this using the `sudo` command to create a file as another user on your system. (Note: this command is normally used to run commands as the root user, but can actually be used to run a command as any user on the system. Consult the man page to figure out how to do this.)
1. Create a group called, say, `linux_study` for all the linux study group members you created (if you didn't create any, creat some accounts now, but no need to worry about setting up SSH keys and all that jazz -- you just need multiple user accounts to work with). Add yourself and all the users you created to this group. (This exercise and the next closely follow the books example of creating a shared music directory.)
1. Create a directory where this group can share documents with each other called, say, `linux_group_docs`. `/usr/local/share` is a reasonable place to put this.
   - The directory will need appropriate group ownership and permissions so that users in the `linux_study` group can add files to it.
   - When a user adds a file to this directory, other users from the group (but no one else) should be able to edit it.
   - If a user creates a subdirectory to edit files, other users should be able view the contents of this subdirectory and add files to it.
   - Verify this all works using the sudo command as in exercise 2.
1. Who is allowed to create, rename, or delete files in the shared directory?
1. What does the executable permission mean for a directory?
1. What permissions does the `irb` file have? (Hint: you'll have to find where `irb` lives using the info from chapter 3. It may be a symbolic link on your system -- TLCL discusses permissions for symbolic links.)
1. Change the permissions on `irb` to 754. Does the fact that it's a symbolic link change how you go about doing this? What does this do? What impact does it have on your ability to use `irb`? Put back the correct permissions.
1. DON'T DO THE FOLLOWING, IT'S JUST A THOUGHT EXPERIMENT: What would happen if you changed the owner and group of the `sudo` command to your own user accont?
