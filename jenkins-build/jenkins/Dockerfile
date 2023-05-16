# Use an official Jenkins LTS image as the base
FROM jenkins/jenkins:lts

# Switch to the root user
USER root

# Install necessary tools and libraries
RUN apt-get update && apt-get install -y \
    curl \
    git \
    python3 \
    python3-pip \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Install Docker
RUN curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

# Install Helm
RUN curl https://baltocdn.com/helm/signing.asc | apt-key add -
RUN echo "deb https://baltocdn.com/helm/stable/debian/ all main" | tee /etc/apt/sources.list.d/helm-stable-debian.list
RUN apt-get update && apt-get install -y helm

# Switch back to the Jenkins user
USER root

# Install Jenkins plugins using the plugins.txt file
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
# RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Configure Jenkins with predefined settings
# COPY config.xml /usr/share/jenkins/ref/config.xml

# # Copy custom Groovy scripts for Jenkins initialization
# COPY init.groovy.d/ /usr/share/jenkins/ref/init.groovy.d/

# # Copy jobs and other configuration files
# COPY jobs/ /var/jenkins_home/jobs/
# COPY config/ /var/jenkins_home/config/

# Expose the Jenkins web interface port
EXPOSE 8080

# Set the Jenkins home directory as a volume
VOLUME /var/jenkins_home
