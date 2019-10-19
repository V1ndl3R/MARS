Steps to Create EC2 Instance
----------------------------------

Go to www.letsencrypt.com (free service)

First, head to AWS and find the EC2 management console.

Select the option for Launch a New Instance.

Configure the instance to using Ubuntu 18.04, x64 bit, with the default resources provided under the free offering.

It is important to select the VPC created previously with the network subnetted properly ahead of time. This occurs in the Configure Network tab during instance creation.

Once the instance is launched, you are given a key.pem for your EC2 instance. Do not lose this key!!

Configure a PUTTY instance to login to your EC2 instance using it's public DNS, default user (ubuntu), with the key provided to you in the previous step.

Next, add users for your team members with the following commands:

    $ sudo adduser janetester --disabled-password
    $ sudo su - janetester
    $ mkdir .ssh
    $ chmod 700 .ssh
    $ touch .ssh/authorized_keys
    $ chmod 600 .ssh/authorized_keys

Then have the key associated with a partcular team member saved in the 'authorized_keys' file for that team members' account.

At this point, you have created the EC2 instance within a custom subnetted network, and granted secure access without the need of a password for your team members.

Team members can use the following within a terminal to create an ssh connection with the EC2 instance:

    $ ssh -i /file/path/to/privatekey.pem janetester@ec2-54-188-166-137.us-west-2.compute.amazonaws.com

There are many ways to allow access to your server. Cloud-init is another way to allow access.

## Cloud-Init

First, make sure your EC2 is stopped.

Select 'Actions' and then edit user data. 

Within the text field, paste the following script with changes made to the username and ssh-rsa key fields.

    #cloud-config
    cloud_final_modules:
     - [users-groups,always]
    users:
      - name: janetester
        groups: [ wheel ]
        sudo: [ "ALL=(ALL) NOPASSWD:ALL" ]
        shell: /bin/bash
        ssh-authorized-keys: 
        - ssh-rsa AB3nzExample

This allows a new user to connect to your EC2 instance and is granted the same permissions as the default user you used to initially connect.
