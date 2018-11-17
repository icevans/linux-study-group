# Things You Should Get Done on Your New Server

1. *Digital Ocean: Change the root password from the default that you got from Digital Ocean.*

   *AWS Lightsail: Root login is disabled by default and this step is unnecessary.*

WHY: Digital Ocean emailed this password to you in plaintext. Anyone watching network traffic could have seen that and would then know the root password to your machine. This means they could log in as root over SSH. (The root user has all privileges, so they could do anything they wanted to your machine.) Even if you disable password login, if they managed to login as a regular user (maybe one of your users accidentally exposes their private key and a bad actor gets their hands on it) then they have the root password and so could switch to the root account using `su root`. Once again, they would become `root` and so do anything to your machine.

2. *Digital Ocean & AWS: Create a user account for yourself.*

WHY: Generally, you want to log in as a normal user. Because the root user can do anything, it's very dangerous to login as root... if you mistype one little command you could potentially destroy your whole system. Make a good strong password and don't lose it!

AWS WHY: Although by default you don't login as 'root' on AWS, and thus are not susceptible to the issues stated above, you are set up as a default user depending on the distro you choose during the instance creation process (Example: Ubuntu distro = 'ubuntu' as username). It's a worthwhile experience to create your own user account with a more meaningful username. (f.y.i. It's much simpler to create a new user account than to change the default username.)

3. *Digital Ocean & AWS: Add your user new account to the `sudo` group*

WHY: You won't be logging in as root anymore, but it's your machine and you'll need root privileges to edit certain system files or run certain commands. Adding yourself to the `sudo` group means that you can put `sudo` in front of a command to run that command with root privileges... see Chapter 5 of The Linux Command Line for details. You have to be logged in as the root user in order to do this) You use the `usermod -a -G sudo your_username` command for this... the `-a` option says you want to add something to a user account, and the `-G` option says it's a group you're adding. You'll need to be logged in as `root` to accomplish this. You can verify that you've succeeded by logging into your account and trying to run a command with `sudo`, e.g. `sudo ls /root`, and also by typing `groups` which list all the groups your user account belongs to. [More information about `usermod` and groups.](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/)

AWS WHY: The default user account will already be set up as part of the `sudo` group, but if you create a new user as recommended in Step 2, you will need to add the new user to the `sudo` group.

4. *Digital Ocean & AWS: Generate Public Keys, Configure Public Key Authentication for Your User* 

WHY: Public key authentication is much more secure than password authentication, and also convenient because you don't have to type a password when you login. [Decent instructions on how to do this](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server) *Important Note*: If you set a passphrase on your key when you created it, you will get prompted to enter this passphrase when you try to connect to your server. This is still key-based login, the password is just need so your own machine can decrypt your key to use it for login.



AWS WHY: The key gen process detailed in the Digital Ocean link above is universal and works for AWS. After completing key generation, follow the instructions at: [AWS: How to complete Public Key Authentication](https://hackernoon.com/add-new-users-to-ec2-and-give-ssh-key-access-d2abd084f30c). Begin at the instructions: "Next, we switch the shell session to the new account:", to setup public key authentication for the new user. You will ssh into your server as the default user to complete this step (Example: ssh ubuntu@ip_address). **IMPORTANT** People understandably get confused on this step as to where to do what. Please read both the Digital Ocean and HackerNoon instructions carefully as to what machine, and to what user, to perform what operations!

5. *Disable Password Login to Your Server, Disable Root Login to Your Server (Only After Step and 4!)*: 

   *AWS Lightsail: Follow the steps below, but you should find these abilities already disabled by default.*

WHY: Now that we have it working, we want to disable password authentication, since password authentication is far less secure. Once it's disabled, people can't point password guessing bots at our server and try to break in. We're also explicitly disallowing people from trying to log in as root over ssh. We really really don't want anyone to get root access to our server. This may be overkill if we've already disabled password login and never added any authorized keys for the root user account, but it doesn't hurt to be extra sure, and anyway we should make the config file say exactly what we want.)

*Steps for this:* Open the `sshd_config` file in a text editor by typing: `sudo nano /etc/ssh/sshd_config`. Configuration files live in the `/etc` directory (see chapter 3 of _The Linux Command Line_), and we're going to edit the config file for the `sshd` program: this program runs in the background on your server and listens for requests from other computers trying to connect to your server over ssh. We have to use `sudo` because this file is owned by the `root` user (see chapter 5 of _The Linux Command Line_ to learn about users and file ownership/permissions). In this file, find the line that says `PasswordAuthentication yes` and change the `yes` to `no`. Find the line that says `PermitRootLogin yes` and change the `yes` to `no`. Press `ctrl-o` to save, and press `ctrl-x` to quit the editor.

6. *Digital Ocean & AWS: New_user, `.ssh` directory and `authorized_keys` file setup on your server:*

WHY: You've been able to set up your server and add yourself as a non-root user. Now it's time to allow access to users that you as the system administrator wish to grant access to. The process is very similar to the steps you took to set up your own user account, with a few tweaks.

*Steps for new_user setup:*
- If you haven't already, connect to your server and go to your home directory. `cd ~`
- Create a new user: `sudo adduser --disabled-password new_user` (new_user will be the preferred username you obtain from the spreadsheet.) `--disabled-password` is optional and bypasses setting a password for the user at setup. The user will be able to set their own password later.
- Switch the shell session to the new user: `sudo su new_user` (Remember: new_user = user name from spreadsheet.).
- Go to the new_user home directory (/home/new_user): `cd ~`
- Create the `.ssh` directory for the new_user: `mkdir .ssh`
- Set the appropriate permissions for the `.ssh` directory: `chmod 700 .ssh` This is setting the permission level so that certain other users on the server can't access this directory. (Check chapter 9 of the assigned reading for further info.)
- Create the `authorized_keys` file: `cd .ssh`, `touch authorized_keys`.
- Secure the `authorized_keys` file: `chmod 600 authorized_keys`
- Copy in the new_users public key from the spreadsheet to the `authorized_keys` file: Open nano: `nano`, copy the new_users public key from the spreadsheet, focus the cursor in `nano`, right-click the mouse, `^o`, `<enter>`, `^x`.
- Close the new_user shell session: `exit`

The new_user is now able to ssh into your server! `ssh new_user@your_server_ip_address`

7. **You're All Set!** Now open up _How Linux Works_ and the _The Linux Command Line_ readings and start learning how this stuff works!

### Supplemental Links

- Looking for a more [gradual introduction to using Linux?](https://www.digitalocean.com/community/tutorial_series/getting-started-with-linux).

- [This Digital Ocean tutorial](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04) addresses steps 1 - 3 & part of 4 above.

- Gert van Dijk's blog has information on [creating an 'upgraded' Ed25519 ssh key](https://blog.g3rt.nl/upgrade-your-ssh-keys.html) (as opposed to an RSA key).

- [Servers for Hackers](https://serversforhackers.com/s/start-here) offers a clear video tutorial with notes that covers much of the material above.

