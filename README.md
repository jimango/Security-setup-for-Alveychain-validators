# Security-setup-for-Alveychain-validators
## Notice
First of all this is an unofficial guide for Alveychain validators, meaning I made this as a community member for easier explaining to all that ask in TG chat.
There are many other ways to make a server much more secure, but this is some very basic moves to improve the security on a basic level.

## The explaination
In the Alveychain README docs at their official link https://github.com/AlveyCoin/validator you can find more information how to tighten your securty for the server under `Before You Start`. 
There you can find links which I recommend you to check out.

But the following information at this page will at least get you started with the basics. And hopefully some better understanding before you get on with the rest of understanding the sercutiry layers of running a server.

## The steps we will be doing
We want to make some changes to the server to improve the basic security of our server a bit.


1. Setting up a new user & Giving that user admin rights (sudo rights)

2. Remove the remote login access for the root user. Important to have set up the new user first in step 1.


<i>
This is necessary to make the server more secure for getting hacked by malicious login software or the packages that we will install and use at the server.
I will provide public links to explain each step.
This way you can also learn how to confirm all steps you do from legitim sources. Always check the source and understand what you do when operating in a server environment.
This will make it safer when taking guidance and advices from others that you can not blindly turst.
</i>

## Why
The security of this server is important since it will contain the information required to have control of your validator wallet and setup.

## First - User setup:
In this example we make a user named sammy, you should of course choose some other username that you are comfortable with using.

| Step | Commands                          | Reason                                                                                                                                                  |
|------|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. | `adduser sammy`                     | Adds new user. At the personal information they ask about you dont add any, just keep pressing Enter until the end.                                     |
| 2. | `usermod -aG sudo sammy`            | This gives your new user admin rights, so that you basically can do similar actions like root but without making your server so volunerable.            |
| 3. | `su sammy`                          | Log into that user. You can see this by how the front of the commandline from now on will show the user name instead of root.                           |
| 4. | `cd`                                | Moves you to the home folder of that new user. When installing applications like the validator setup we want to do that in the new user's home folder.  |
| 5. | `sudo apt update`                   | Check if this new user can check for Ubuntu updates                                                                                                     |
| 6. | `sudo apt upgrade`                  | Install any updates if there is any.                            

If you are able to do all these steps you have set up a new user (which you can log in with using Putty), and this new user have all the rights it needs to install applications like the Alveychain validator setup.

This explaination is similar to that you find in pages like, or similar google searches: 

https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-22-04-quickstart


## Secondly - Remove access for root to log in remotly:
This makes it harder for malicious login software to get access to your server by randomly testing for passwords matching the user root.

| Step | Commands                          | Reason                                                                                                                                                  |
|------|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. | `sudo pico /etc/ssh/sshd_config`                                                                         | Opens the file sshd_config from its folder. Using the sudo command gives your new user (see above) access to save the file after completion. You can use other editing options like `vi` instead of `pico` but personally I like pico even though I know many prefer vi or similar.       |
| 2a.| Use arrows at the keyboard to search for the `PermitRootLogin yes`and change it to ´PermitRootLogin no`  | This removes the posibility for root to log in remotly using putty or similar software.       |
| 2b.| If it says `#PermitRootLogin no` with a # infront you simply remove the #`                                                                         | The sign # in such files deactivate that line, so removing the # will make that command valid. In most cases you dont need to do this step 2b, and you only have to do step 2a. This step is only if that line has a # infront of it. |
| 3. | To close the file after its edited as in step 2, press `Ctrl+X` at the keyboard, follow by pressing `Enter` to save as the same original filename.   | This should bring you out of the file you were editing and back to the command line. Where we can continue our commands. |
| 4. | `systemctl restart sshd` <br> OR <br> `/etc/init.d/sshd restart`                                                   | Each of these commands will restart the loging software so that the changes will be active when login in the next time. If the first does not work, you should try the second. |
| 6. | Next time you log into the server you should no longer be able to login as root, you will need to enter your new username to be able to login to your server for the future.                  | This is a basic setup to improve your servers security        


This explaination is similar to that you find in pages like, or similar google searches: 

https://www.tecmint.com/disable-or-enable-ssh-root-login-and-limit-ssh-access-in-linux/


## Finally 
After having done this you can continue with following the directions of how to setup the Alveychain validator setup as explained in: 
https://github.com/AlveyCoin/validator

And please do check the links at the top of their page in the `Before You Start` section, it contains some more info on how to improve the security even further. 
But these instructions here at my page will have gotten you started with the very basic. I might improve this page with even further instructions later on, to make it easier to get your mind around if you are new to all these things.


## If you already installed validator setup using root
If you already set up the validator setup using root, you must make sure to safely store the keys and info to not loose access to that wallet (if you already transfered money there)
You will need to do this again using the new user that you have created. Which means it will set up a whole new wallet with new keys (private and public)
So if make sure to keep control of your investment while setting it up again under the new user.
There is no easy or recommended way to transfer the root setup onto your new user, you need to start again with the new user.

I will add an explaination on how to finally remove the root installation of the validator setup here soon..
