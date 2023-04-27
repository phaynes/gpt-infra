# Dockerfile
FROM registry1.dso.mil/ironbank/redhat/ubi/ubi9:latest
# FROM docker.io/library/almalinux:latest

# Install necessary packages
RUN dnf install -y openssh openssh-clients openssh-server 
RUN dnf install -y python3-pip gcc python3-devel && \
    pip3 install --upgrade pip && \
    pip3 install ansible boto3

# Set up the working directory
WORKDIR /ansible

# Copy the Ansible playbook and configuration files
COPY create_vm.yml /ansible/
COPY ansible.cfg /ansible/
COPY inventory /ansible/
COPY 1SkyDemo.pem /ansible/
COPY .ssh/id_ed25519 /root/.ssh/
COPY .ssh/id_ed25519.pub /root/.ssh/


# Run the Ansible playbook
CMD ["ansible-playbook", "create_vm.yml"]
