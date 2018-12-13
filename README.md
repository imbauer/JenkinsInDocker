# Jenkins Deployment inside of a Docker Container
Using NGINX as a Reverse Proxy to connect the container (Jenkins) to the outside world (Github)
# 1.
---> Go to this website: https://engineeringtgr.com/freedns/ 
... Extract the .exe from the .zip file ... Run the .exe
... $ ngrok http 192.168.99.100:8080     (Or whatever ip_address:port that your docker container is running on)
# 2.
---> In jenkins.conf replace all {{ ngrok_id }} with the forwarding id from the terminal in #1
... On the line proxy_pass http://jenkinsdocker_master_1:8080; , the url comes from the name of the jenkins-master container
... Check this by running $ docker ps
... On Github set Webhook as follows: http://{{ ngrok_id }}.ngrok.io/github-webhook/
... Setup a Jenkins Job with the following configurations:
... Check the Github Project box ... Project url = https://github.com/imbauer/TestJenkins/
... Check the Git box ... Repository URL = https://github.com/imbauer/TestJenkins.git
... Check Github hook trigger for GITScm polling
... Save
# 3.
---> Now when you push a commit to this Github Project, a build should automatically begin for you :D
# 4. Don't forget to install Docker!
