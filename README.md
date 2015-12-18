###Server Info
IP Address: 52.27.134.129 
SSH Port: 2200

### Application URL
You can access the hosted application at the following address: [http://ec2-52-27-134-129.us-west-2.compute.amazonaws.com/](http://ec2-52-27-134-129.us-west-2.compute.amazonaws.com/)

###References Consulted
####UTC Time
https://help.ubuntu.com/community/UbuntuTime#Using_the_Command_Line_.28terminal.29
ssh grader@52.27.134.129 -p 2200 -i /c/users/pcmar/.ssh/udacity_key.rsa

####Initial Set-up
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-12-04

####Postgres
https://help.ubuntu.com/community/PostgreSQL

####Flask
[http://flask.pocoo.org/docs/0.10/deploying/mod_wsgi/](http://flask.pocoo.org/docs/0.10/deploying/mod_wsgi/)
[http://flask.pocoo.org/docs/0.10/patterns/packages/](http://flask.pocoo.org/docs/0.10/patterns/packages/)

###Installed Software
- ntp - To keep time up to date
- Apache2
- mod_wsgi
- python-psycopg2
- python-pip
- Flask
- SqlAlchemy
- postgresql
- git

####Installed through pip
- ouath2client
- requests
- httplib2

###Configuration
Just as a preface, I really meant to take better notes as I went along, but then got lost in trying things, so this might be a little rough.

####UFW firewall settings

The table below contains the ports opened in the application firewall

| To | Action  | From |
| --- | ------  | ---- |
| 2200/tcp | ALLOW | Anywhere |
| 80/tcp   | ALLOW  | Anywhere |
| 123/udp | ALLOW   | Anywhere |
| 2200/tcp (v6)  |  ALLOW  | Anywhere (v6) |
| 80/tcp (v6)  | ALLOW | Anywhere (v6) |
| 123/udp (v6) | ALLOW | Anywhere (v6) |

####Catalog App
I had to turn the app into a python package to make it play nicely with WSGI. `catalog.py` became `__init__.py`. I also changed the database from sqlite to postgresql. The only changes I had to make to my `database_setup.py` file were to the set the engine to a postgres database, and add a UNIQUE constraint to the filename column on my `photo` table.

After copying the app to my AWS server, I learned that I had to include the full path to any file or folder the app needed to access. For example my Google Plus and Facebook client secrets, and the folder for uploaded photos.

I also had to adjust the permissions for the upload folder in order for the app to work properly. They are currently set to 755.
