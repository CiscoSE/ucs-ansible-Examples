# Using the CENTOS container from the docker library
FROM centos:8

# Requirements for Ansible and the ucs sdks
RUN yum install epel-release python3 python3-pip git vim -y && \
pip3 install --upgrade pip

# Install the Ansible and UCS compenents.
RUN pip3 install ucsmsdk imcsdk xmljson lxml ansible


