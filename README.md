#################################################################
**Group Mars**
#################################################################



################
An Ansible playbook is an organized unit of scripts that defines work for a server configuration managed by the automation tool Ansible. 


###############
Ansible is a configuration management tool that automates the configuration of multiple servers by the use of Ansible playbooks. 



##What will playbook do
1) Install apache2
2) Update apache2
3) Pull Repo for Group Mars
4) Rename current "index.html" to "index.html.old"
5) Copy Group Mars "index.html" to web server root directory
6) Copy all required files from repo to web server root directory
7) Remove repo
8) Restart apache2 Server



##Requirements:
1) Upload your public ssh key to the hosts
2) Make sure your private ssh key has correct permissions
	* chmod 400



##Usage

1) Install ansible
	* sudo apt-get install ansible
2) Go to /etc/ansible/hosts
	* Remove "#" in front of "webservers" to enable it
	* Add hosts under webservers
3) Run the Playbook
	* ansible-playbook --private-key=<your-private-key> <ansible_file_name> -u <username> -k --ask-become-pass

	* Set "--private-key" to your ssh private key
	* Set "-u" to your username
	* "-k" will require password for ssh key
	* "--ask-become-pass" will require root password to get privileged access 
