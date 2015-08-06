# skelUserDirNginx

The skeleton directory template, which contains files and directories to be copied in a new user's home directory, when the home directory is created by useradd. 

This option is only valid if the -m (or --create-home) option is specified.  

If this option is not set, the skeleton directory is defined by the SKEL variable in /etc/default/useradd or, by default, /etc/skel.

This is my version of what the users home dir should look like.. Other people might have a different opionion.

This should work and be complementary with [my (getafixx's) admin scripts repo](https://github.com/getafixx/admin_scripts)

So you want to have a user;s home dir set up properly you need to do one of two thing.

1) you can add the new user 

```
useradd test123
```

but this will not create the home directory, so you could create it like this...

```
cd /home

#clone the repo
git clone --no-checkout https://github.com/getafixx/skelUserDirNginx.git /home/test123

#set correct permissions
chown -R test123:www-data /home/test123/

```

OR if you set up the 

```
/etc/skel
```
like so (as root)

``` 
#remove the current dir
rm -rf /etc/skel

#clone the repo
git clone https://github.com/getafixx/skelUserDirNginx.git /etc/skel

#get rid of git info...
rm -rf /etc/skel/.git

```
Once this is done you can then call the **useradd** command

```
useradd --create-home --skel /etc/skel/ -gid 31 -s /bin/bash test123

where the --create-home will create the user's home dir (/home/test123)

--skel /etc/skel/ to use this as the skeleton files for home dir

-gid 31 sets the group of this user to be www-data

-s /bin/bash sets the shell for user

```
