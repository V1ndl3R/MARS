Steps to Generate TLS Certificates
----------------------------------

Go to www.letsencrypt.com (free service)

Click on the "Get Started" button

In the "With Shell Access" section, click on "Cerbot" which should a font color of blue.

You will be directed to Certbot's Website.

On the main page, you will see the option  "My HTTP" website..."

Select which software is running (Apache for this group) and which system is being used (Ubuntu 18.04 for the server).

After selecting the correct software and OS, you will be redirected to a guide on how to install certbot via command line. It will be under the "default" tab.

First, SSH into the ec2 instance. Make sure you have sudo privileges.

Next, add Certbot PPA with the following commands:

    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo add-apt-repository universe
    $ sudo add-apt-repository ppa:certbot/certbot
    $ sudo apt-get update

Then is stall Certbot:

    $ sudo apt-get install certbot python-certbot-apache

Next, Choose the option to get and install certificates:

    $ sudo certbot --apache

Enter the domain...

!! Choose the option to redirect to secure HTTPS access... !!

You should then see a "Congratulations!" message stating the certificate has been created.

Restart apache.

Go to a browser to see if the site is secure.

I ran into an issue where only www.cit480mars.net was secure, but our original domain cit480mars.net wasn't secure.

I was creating and deleting new certificates and ran into the issue of reaching the weekly limit of 5 certificates per week.

I will have to wait exactly 7 days from 10/10 to try again.

It is now 10/17 and I was able to create new certificates again.

The professor stated that securing www.cit480mars.net is acceptable, but I'm still trying to find a way to secure both.
Someone mentioned that editing the .config file will help complete the task, but I couldn't figure it out.

I found a command online that let's the user change the domains within the certificate:

      $ sudo certbot certonly --cert-name www.cit480mars.net -d cit480mars.net,www.cit480mars.net

      ****If you want to secure 2 domains, separate them by a comma.

After running the command, both domains are not secure when typing them in.
They don't get redirected to HTTPS.

However, www.cit480mars.net becomes secure when manual "typing https://" before the domain.

I've tried creating a new certificate, but the issue doesn't get resolved.
I believe I'm close to reaching the weekly limit again, which forces me to stop troubleshooting.
