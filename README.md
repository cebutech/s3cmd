## Setup Configure Amazon s3cmd


## Overview

In this article, we will show you how to setup and configure the s3cmd tool for Amazon S3.

For this article, you will need SSH access to your account.

    1) Login to your account using your preferred SSH client.
    2) Lets make a folder so we can download all the files we need.

Create the dir

	mkdir s3downloads

Now lets move into this new folder…

	cd s3downloads

Now we need to download the Amazon s3cmd tool.
	
	**for the latest version of the tool please visit http://s3tools.org/s3cmd

	wget http://sourceforge.net/projects/s3tools/files/s3cmd/1.0.0/s3cmd-1.0.0.zip

Lets unzip it and move into the folder.

	unzip s3*zip

	cd s3*

Now its time to install it.

	python2.6 setup.py install --user

We need to move the file into a better folder, so lets do that now.

	mkdir ~/bin

	cp s3cmd ~/bin

	cp -R S3 ~/bin

Lets do some cleanup real fast.

	cd

	rm -r s3downloads

Lets edit our bashrc file so it knows we have installed the s3cmd tool

	vi ~/.bashrc

and add the following to the end…

	if [ -d "$HOME/bin" ]; then
	PATH="$HOME/bin:$PATH"
	fi

Now we need to source the bashrc file so the server knows we changed it.

	source ~/.bashrc

Now its time to configure the s3cmd tool. We can do this by running the following command.

	s3cmd --configure

    Enter your Amazon S3 Access Key
    Enter your Secret Access Key
    
Note: Both of these can be found on the Security Credentials page at the following link: https://portal.aws.amazon.com

Now we need to enter a password (NOT the same one for amazon account ) that will be used to encrypt the local configuration files.
When asked for the path to gpg, just press enter.
If you would like to use HTTPs (recommended) type yes when prompted. Please note that you do NOT need a SSL certificate to use this https function.

	Test the account by typing “y” (when prompted) then pressing enter.

If everything connected correctly, enter “y” when prompted to save the settings. If not, please re-try the configuration.
That’s it! You now know how to install the Amazon s3cmd tools. Below we will show you some of the basic commands you can use with this tool.

 

Commands

    mb
        Command: s3cmd mb
        Description: This command makes a new bucket.
        Example: s3cmd mb s3://newbucket
    rb
        Command: s3cmd rb
        Description: This command removes a bucket.
        Example: s3cmd rb s3://buckettoremove
    ls
        Command: s3cmd ls
        Description: This command lists all file. You can also tell it to check a path/bucket
        Example: s3cmd ls
        Example 2: s3cmd ls s3://buckettocheck
    la
        Command: s3cmd ls
        Description: Lists all files in all buckets
    put
        Command: s3cmd put
        Description: This command puts/uploads a file to the path your specify.
        Example: s3cmd put ~/filetoupload.txt s3://buckettouploadto
    get
        Command: s3cmd get
        Description: This is the same as the put command but in reverse.
        Example: s3cmd get s3://bucket/filetodownload.txt ~/locationtoputit
    del
        Command: s3cmd del
        Description: This command deltes a file on the S3 server.
        Example: s3cmd del s3://bucket/filetodelete.txt

