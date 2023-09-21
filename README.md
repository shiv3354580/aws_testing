# ci-cd-configurations-files




$ wget https://Bucket-name.s3.Region-identifier.amazonaws.com/latest/install


##### Next up, we need to change the permission on the install file we will get after running the command above.

$ chmod +x ./install

##### Finally, to install the codedeploy-agent, run this command:

$ sudo ./install auto > /tmp/logfile

###### Here we are logging the output of the installation to the /tmp/logfile file. To check if the codedeploy-agent is running, enter this command:
$ sudo service codedeploy-agent status

###### If it is not running, enter this command to start the codedeploy-agent service:

$ sudo service codedeploy-agent status



/////////////////////creating cicd pipeline ///////////////////////////

steps
IAM roles
ec2 instance
code deploy installation
code structure
configuration files
code pipeline

step1 // creating iam role
IAM --> roles --> create roles
choose --> aws service --> use case EC2 --> Ec2
click next 
search for awscodedeploy
selection option of aws code deploy
click next
enter role name 
create role
again create role
select aws service
choose a service to view use case --> codedeploy --select code deploy only
enter role name ( a different one )
create role
////////////first step done ///////////////
///////////// create ec2 instance /////////////////
eneter server name
select ubutntu
create key pair ( know well to connect with terminal using .pem key)
choose allow requiest from http traffic from internet
launch instance
go to dashboard select instance
click on actions --> security --> modify iam role --> choose iam role-- select codedeploy role
update iam role
reboot instance
//////step 2 complete //////////////
/////////step 3 code deploy installations///////////////
click on connect connect with ssh

first command
chmod 400 x-downloader-server.pem
second commadn
ssh -i "x-downloader-server.pem" ubuntu@ec2-3-108-185-193.ap-south-1.compute.amazonaws.com
sudo apt update
sudo apt install ruby-full
sudo apt install wget 

wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
.....................


 
Next up, we need to change the permission on the install file we will get after running the command above.

$ chmod +x ./install
Finally, to install the codedeploy-agent, run this command:

$ sudo ./install auto > /tmp/logfile
Here we are logging the output of the installation to the /tmp/logfile file. To check if the codedeploy-agent is running, enter this command:

$ sudo service codedeploy-agent status
If it is not running, enter this command to start the codedeploy-agent service:

$ sudo service codedeploy-agent status
//////////////////////////////////////////////////////////
project structure 
add configuration files
https://github.com/rashiddaha/ci-cd-configurations-files.git -- configuration file link
move files in project directory
after doing chagnes 
////////////step 4 //////////
code deploy pipeline
search for codepipeline
go to build -- getting started 
create project 
project name
select provider -- github
select public repository
connect with github
page repository git url
operating system  --> ubutntu
runtime --> standard
image --> standard6.0
choose new service role
use a buildspec file
create build project
click on applications
application name --> any name
compute platforma --> ec2/on-primises
create application
click on --> create deployment group
deployment group name
service role --> aws code deploy role 
deployment type --> inplace
environment configurations
select --> amazon ec2 instance
key -- name value -- django-server
deployment settings 
codedeplydefaultaallatonce
disable load balancer
click on create deployment group
/////////////////////////////
go to codepipeline --> pipelines create new pipeline
enter pipeline name
choose default location
click on next 
select provider --> github version 1 -- auth done
enter repo name 
enter branch
chose github webhooks
click next
build provider 
aws codebuild
project name --> chose project namee
choose --> single build
next
deploy provider -- aws code deploy
region
application name --> choose app name
depployment group -- chose one
 next
create pipeline

//////// without pipeline
search for iam
select aws
select ec2
search for codefordeploy select first 
enter name for role --> ec2codedeploy
same for new role select codeDeploy --> codedeployrole

///create security groups
inbound rule 
ssh 000000
http 00000
http for ipv6
//////
i create this security group because when i will create a server
i have to chose this options to create security group but if now i have
already created security group i will chose option select security group

///step 2 launch instance 
launcha instance of ubuntu
/// step 3 connect with instance using ssh key which is downloaded with 
.pen extentions
/// after connect with server using terminal 
sudo apt-get update
sudo apt-get upgrade
python3 --version
install python virtual environment
 apt-get install python3.10-venv
to remove directory change the permission first
///install nginx
sudo apt-get install nginx
pip install gunicorn
after this the nginx page will appear on the side address

 1  ls
    2  python3 -m venv env
    3  ls
    4  source env/bin/activate
    5  pip3 install django
    6  git clone https://github.com/shiv3354580/aws_testing.git
    7  ls
    8  cd aws_testing/
    9  ls
   10  python3 manage.py runserver 0.0.0.0:8000
   11  cd ..
   12  ls
   13  clear
   14  sudo apt-get install nginx
   15  pip install gunicorn
   16  pip list
   17  sudo apt-get install supervisor
cd /etc/supervisor/conf.d/
sudo nano gunicorn.conf

[program:gunicorn]
directory=/home/ubuntu/aws_testing
command=/home/ubuntu/env/bin/gunicorn --workers 3 --bind unix:/home/ubuntu/aws_testing/app.sock elevate.wsgi:application
autostart=true
autorestart=true
stderr_logfile=/var/log/gunicorn/gunicorn.err.log
stdout_logfile=/var/log/gunicorn/gunicorn.out.log

[group:guni]
programs:gunicorn


//////////////////////////////////
  cd /etc/supervisor/conf.d/
   39  ls
   40  cd /etc/supervisor/conf.d/
   41  sudo nano gunicorn.conf
   42  sudo mkdir /var/log/gunicorn
   43  sudo supervisorctl reread
   44  history
  sudo supervisorctl update
   46  sudo supervisorctl status

go to etc directory and then nginx

 sudo nano nginx.conf

change user to root
go to sites availabel director and create django.conf file 
django.conf changes 
server{

        listen 80;
        server_name 43.204.230.55;

        location / {

                include proxy_params;
                proxy_pass http://unix:/home/ubuntu/aws_testing/app.sock;
        }
}

make chages in settings file change to allowed hosts

 sudo touch django.conf
   60  sudo nano django.conf
   61  sudo nginx -t
   62  sudo ln django.conf /etc/nginx/sites-enabled/
   63  sudo service nginx restart
   64  cd ..
   65  ls
   66  cd ..
   67  cd home
   68  ls
   69  cd ubuntu/
   70  ls
   71  cd aws_testing/
   72  ls
   73  cd elevate/
   74  ls
   75  sudo nano settings.py
   76  sudo service nginx restart
   77  sudo nano settings.py

reboot the instance after changes 

