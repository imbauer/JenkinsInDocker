# Jenkins Deployment inside of a Docker Container
Using NGINX as a Reverse Proxy to connect the container (Jenkins) to the outside world (Github)
# 1.
---> Run the following command to expose the locally hosted instance to the exposed url jenkinsindocker.serveo.net
... $ ssh -R jenkinsindocker.serveo.net:80:192.168.99.100:80 serveo.net
# 2.
---> In jenkins.conf replace all {{ ngrok_id }} with the forwarding id from the terminal in #1
... On the line proxy_pass http://jenkinsdocker_master_1:8080; , the url comes from the name of the jenkins-master container
... Check this by running $ docker ps
... On Github set Webhook as follows: http://jenkinsindocker.serveo.net/github-webhook/
... Setup a Jenkins Job with the following configurations:
... Check the Github Project box ... Project url = https://github.com/imbauer/TestJenkins/ (replace with your github project)
... Check the Git box ... Repository URL = https://github.com/imbauer/TestJenkins.git (replace with your github project)
... Check Github hook trigger for GITScm polling
... Save
# 3.
---> Run the following command to expose the locally hosted instance to the exposed url jenkinsindocker.serveo.net
... $ ssh -R jenkinsindocker.serveo.net:80:192.168.99.100:80 serveo.net
# 4.
---> Now when you push a commit to this Github Project, a build should automatically begin for you :D!