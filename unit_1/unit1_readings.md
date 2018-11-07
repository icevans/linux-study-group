## Part 1: History, Important Concepts, Users and Permissions, Standard Directory Structure

Our goal here is to understand what Linux is and some historical context, as well as understand some important concepts like 'kernel' and 'shell'. Additionally, we'll learn how the Linux filesystem is standardly organized, and how to work with permissions, users and groups. In order to do this, and to set us up for the rest of our explorations, I propose that we each set up our own little remote Linux machine to have as a lab, where we can tinker and not worry about breaking stuff.  This will also introduce you those of you have never done so to working with remote servers over SSH, an essential skill for web developers.

You can set up your Linux machine on whatever provider you like: Digital Ocean, Linode, Amazon LightSail, etc. I'd recommend Digital Ocean just because their documentation is truly exceptional. This will cost you around $5/month — I hope that's not prohibitive to anyone, but if it is, message me and we'll figure something out.

So the first activity will be to get your Linux server setup so that you can SSH into it, along with some basic security precautions (one of the readings is a Digital Ocean article that walks you through the steps). I think a fun secondary activity would be for us all to share our public keys, then we can all create (limited) user accounts for each other on our servers. If anyone has trouble getting started with any of this, ask questions on Slack. Your little server will be the perfect place to experiment with all of the tools and topics we go through.

### Readings

-  [This video](https://www.youtube.com/watch?v=-rPPqm44xLs&t=0s&list=PLwtBDPwjv7bxDPZqIFw8JHk9NXewABX28&index=5) on the history of Unix 
- Digital Ocean [history of linux article](https://www.digitalocean.com/community/tutorials/brief-history-of-linux)
- Digital Ocean [initial server setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04?utm_source=Customerio&utm_medium=Email_Internal&utm_campaign=Email_UbuntuDistroNginxWelcome&mkt_tok=eyJpIjoiTm1Rd01tWmhPVGRqWXpNNCIsInQiOiJTMmtlekp4SUJkYVB6QW42S1FLTmNXcnNsZ0RweGhEYndSY2J4VERrV3lVeFJsWDVZUFRkQUZGcEw5RDNIRDFhYmQ3NzNVakgrTkhIUUVZM1VCbWE5ZHVMdUQxbUZ3blppbU85Z0w0STlQOGFoXC95YXF0aFpKT1ZXUVk5RForWGYifQ%3D%3D)
- [How Linux Works](https://nostarch.com/howlinuxworks2), chapter 1 (What's a Kernel) (This is for background and high level conceptual understanding, if this feels too "computer-sciencey" don't worry about learning to depth)
- [The Linux Command Line](https://nostarch.com/tlcl), chapter 3 (Exploring the System)
- The Linux Command Line, chapter 9 (Permissions)

### Optional/Supplemental:

- Digital Ocean [getting started with linux series](https://www.digitalocean.com/community/tutorial_series/getting-started-with-linux)