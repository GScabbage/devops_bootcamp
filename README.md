# DevOps Environment Creation in Vagrant
### Preparing the environment
- SSH into the environment at run `sudo apt-get update -y`
- Followed by `sudo apt-get upgrade -y`
#### Preparing second terminal to run test
- Open another gitbash terminal
- Navigate to the location of the rakefile, in this case in spec-tests
- In this terminal run `gem install bundle`
- Then run `bundle`
- This will allow the use of the rakefile and gemfile to check the app requirements are met
### Using Tests to ensure all modules are installed
- Run `rake spec`, this will reveal the missing packages
- 3 failures should appear, or maybe 4 if you didn't have nginx install with `provision.sh`
- If that is the case then return to your ssh terminal and install nginx with `sudo apt install nginx -y`
- As for the other 3 failures, 2 will be for nodejs and 1 will be for pm2
- First run `sudo apt install nodejs -y`
- This will fix the first nodejs failure but not the second the specific version it requests is not installed
- Now run `sudo apt-get install python-software-properties` followed by `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`
- This gets the specific version from the nodjs source website
- Then run `sudo apt install nodejs -y` again to install it
- There will now only be 1 failure left
- Run `sudo npm install pm2 -g`, this will install pm2 meaning no more failures remain
- (If you want pm2 to actually work use this command instead `sudo npm install pm2@^3 -g`)
### Final preparations to run the app
- Inside of your ssh terminal navigate to `/app/app`, if this is not there then make sure the synced folder is in your vagrant file and is correct
- Once there run the command `npm install`, this will install the relevant packages for the app to run correctly
- If it has alot of deprecation erros then rerun `sudo apt-get updates -y` and `sudo apt-get upgrade -y`, this should fix it if not it shouldn't affect it running anyway
- Finally run the command `npm start`, this will start the app
### Connecting to the app
- Got to your chosen web browser on your local machine
- Connect on the ip you gave on port 3000 which should be `192.168.10.100:3000`
- If this displays the app start page then everything is setup correctly


# **Linux Commands**
- Who am I `uname` or `uname -a`
- Where am I `pwd` will display current location
- How can I list contents including hidden files `ls -a`
- Remove a file `rm filename` or `rm -rf filename`
- Create a file `touch filename` or `nano filename`
- Make a directory `mkdir dir_name`
- Navigate inside a directory `cd name_dir`
- List all processes running `ps`
- Kill a process `kill process id/s`
- Wildcard is used to deal with multiple files with the same extenstion `*`
- File permissions `+x executable` `+r read` `+w write` use these with `chmod` will apply to all groups
- Check permissions `11`
- Change permissions `chmod permission_wanted filename`
- Copy file or folder command in Linux `cp filepathtocopy destinationtocopyto`
- Cut Paste - Move file or folder `mv`
- How to use piping | `ls | head -2`

#### **Variable and Environment Variable**
- How to check env var? `env`
- Creating env var `export key=value`
- Use `printenv key` to print a specific variable to the terminal
- To create a persitent env var, in your home directory run `nano .profile` then add `export key=value` then exit the ssh and come back in and the variable will be their permanently  
