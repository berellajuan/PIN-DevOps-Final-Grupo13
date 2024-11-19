FROM jenkins/jenkins:lts

# Configurar usuario y contraseña
ENV JENKINS_USER admin
ENV JENKINS_PASS admin

# Instalar Docker
USER root
RUN apt-get update && \
    apt-get -y install apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
        $(lsb_release -cs) \
        stable" && \
    apt-get update && \
    apt-get -y install docker-ce && \
    usermod -aG docker jenkins

# Instalar kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Mover archivo config y configurar KUBECONFIG
COPY config /var/jenkins_home/.kube/config
RUN mkdir -p /var/jenkins_home/.kube && \
    chown -R jenkins:jenkins /var/jenkins_home/.kube
ENV KUBECONFIG=/var/jenkins_home/.kube/config

# docker run -d -u $(stat -c '%u:%g' /var/run/docker.sock) --network="host" -p 8080:8080 -v jenkinsvol:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins-pin-final jenkins-local:v1