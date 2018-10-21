# Things You Should Get Done on Your New Server

1. *Change the root password from the default that you got from Digital Ocean.*
   *AWS EC2/Lightsail: Root login disabled by default.*

WHY: Digital Ocean emailed this password to you in plaintext. Anyone watching network traffic could have seen that and would then know the root password to your machine. This means they could log in as root over SSH. The root user has all priveleges, so they could do anything they wanted to your machine.) Even if you disable password login, if they managed to login as a regular user (maybe one of your users accidentally exposes their private key and a bad actor gets their hands on it) then they have the root password and so could switch to the root account using `su root`. Once again, they would become `root` and so do anything to your machine

2. *Create a user account for yourself.*

WHY: Generally, you want to log in as a normal user. Because the root user can do anything, it's very dangerous to login as root... if you mistype one little command you could potentially destroy your whole system. Make a good strong password and don't lose it!

3. *Add your user new account to the `sudo` group*

WHY: You won't be logging in as root anymore, but it's your machine and you'll need root privileges to edit certain system files or run certain commands. Adding yourself to the `sudo` group means that you can put `sudo` in front of a command to run that command with root privileges... see Chapter 5 of The Linux Command Line for details. You have to be logged in as the root user in order to do this) You use the `usermod -a -G sudo your_username` command for this... the `-a` option says you want to add something to a user account, and the `-G` option says it's a group you're adding. You'll need to be logged in as `root` to accomplish this. You can verify that you've succeeded by logging into your account and trying to run a command with `sudo`, e.g. `sudo ls /root`, and also by typing `groups` which list all the groups your user account belongs to. [More information about `usermod` and groups.](https://www.howtogeek.com/50787/add-a-user-to-a-group-or-second-group-on-linux/)

4. *Generate Public Keys, Configure Public Key Authentication for Your User* 

WHY: Public key authentication is much more secure than password authentication, and also convenient because you don't have to type a password when you login. [Decent instructions on how to do this](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server) *Important Note*: If you set a passphrase on your key when you created it, you will get prompted to enter this passphrase when you try to connect to your server. This is still key-based login, the password is just need so your own machine can decrypt your key to use it for login.

5. *Disable Password Login to Your Server, Disable Root Login to Your Server (Only After Step and 4!)*: 

WHY: Now that we have it working, we want to disable password authentication, since password authentication is far less secure. Once it's disabled, people can't point password guessing bots at our server and try to break in. We're also explicitly disallowing people from trying to log in as root over ssh. We really really don't want anyone to get root access to our server. This may be overkill if we've already disabled password login and never added any authorized keys for the root user account, but it doesn't hurt to be extra sure, and anyway we should make the config file say exactly what we want.)

*Steps for this:* Open the `sshd_config` file in a text editor by typing: `sudo nano /etc/ssh/sshd_config`. Configuration files live in the `/etc` directory (see chapter 3 of _The Linux Command Line_), and we're going to edit the config file for the `sshd` program: this program runs in the background on your server and listens for requests from other computers trying to connect to your server over ssh. We have to use `sudo` because this file is owned by the `root` user (see chapter 5 of _The Linux Command Line_ to learn about users and file ownership/permissions). In this file, find the line that says `PasswordAuthentication yes` and change the `yes` to `no`. Find the line that says `PermitRootLogin yes` and change the `yes` to `no`. Press `ctrl-o` to save, and press `ctrl-x` to quit the editor.

6. **You're All Set!** Now open up _How Linux Works_ and the _The Linux Command Line_ readings and start learning how this stuff works!
