FROM centos:8

USER root

# Install ansile
RUN yum -y install python3
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
  python3 get-pip.py && \
  pip install ansible --upgrade

# Install jenkins
RUN dnf -y install java-1.8.0-openjdk-devel
RUN yum -y install wget
RUN wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
RUN rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
RUN yum -y install jenkins
RUN yum -y install initscripts

# Start jenkins daemon manually
RUN /etc/init.d/jenkins start

RUN yum -y install openssh-server
RUN ssh-keygen -A
CMD /usr/sbin/sshd -D