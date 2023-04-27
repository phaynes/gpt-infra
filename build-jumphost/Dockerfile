# Dockerfile
FROM registry.access.redhat.com/ubi9:latest 

# Install necessary packages
RUN dnf install -y openssh openssh-clients openssh-server 
RUN dnf install -y python3-pip gcc python3-devel

RUN adduser remote
RUN su remote -c "mkdir /home/remote/.ssh/"

# Set up the working directory
WORKDIR /home/remote

RUN su remote -c "pwd"
RUN su remote -c 'ssh-keygen -t ed25519 -f .ssh/id_ed25519 -P "" '
RUN su remote -c "pip3 install --upgrade pip"
RUN su remote -c "pip3 install ansible boto3"


# Copy the Ansible playbook and configuration files
COPY create_vm.yml /home/remote
COPY ansible.cfg /home/remote
COPY inventory /home/remote
COPY 1SkyDemo.pem /home/remote/
RUN chown -R remote:remote /home/remote

# Run the Ansible playbook
CMD ["ansible-playbook", "create_vm.yml"]
