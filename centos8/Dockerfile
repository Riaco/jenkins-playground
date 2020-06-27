FROM centos:8

RUN yum -y install openssh-server

# Create user and set passwd and make ssh configuration dir to user dir
RUN useradd remote_user && \
  echo "remote_user:1234" | chpasswd && \
  mkdir /home/remote_user/.ssh && \
  chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/autorized_keys

# Everithing in /home/remote_user/.ssh will be owned by remote_user(user):remote_user(group)
RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
  chmod 600 /home/remote_user/.ssh/autorized_keys

# Generate ssh key in container
RUN ssh-keygen -A

# Install mysql cli
RUN yum -y install mysql

# Install aws cli
RUN yum -y install python3 && \
  curl -O https://bootstrap.pypa.io/get-pip.py && \
  python3 get-pip.py && \
  pip3 install awscli --upgrade

RUN rm -rf /run/nologin
# RUN yum -y install sshpass

EXPOSE 22

# Start ssh server
CMD /usr/sbin/sshd -D
