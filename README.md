# README #


## HOW TO RUN ##

	docker run -d atlassian/bamboo-agent-base:latest <<bamboo-url>>
	
<<bamboo-url>> is required for run image.

	
### SUPPORTED VARIABLES ###

	SECURITY_TOKEN (optional) Bamboo security token 
	
usage

	-e "SECURITY_TOKEN=<<security token from Bamboo>>
	
	
### USAGE VOLUMES FOR BAMBOO AGENT HOME ###

Bamboo agent home in container path:

	/home/bamboo/bamboo-agent-home
	
usage

	-v <<path to bamboo home on host>>:/home/bamboo/bamboo-agent-home
	
## EXTENDING BASE IMAGE ##

Example of Dockerfile which extends base image by Maven and Git

	FROM __IMAGE_NAME__
	MAINTAINER Bamboo/Atlassian
	USER root
	RUN apt-get update && \
		apt-get install maven -y && \
		apt-get install git -y

	USER ${BAMBOO_USER}
	RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.mvn3.Maven 3.3" /usr/share/maven
	RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.git.executable" /usr/bin/git