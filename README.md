# DevOps Environment Creation in Vagrant
### Preparing the environment
- SSH into the environment at run `sudo apt-get updates -y`
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
### Final preparations to run the app
- Inside of your ssh terminal navigate to `/app/app`
