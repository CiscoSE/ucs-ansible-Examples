# Using the CENTOS container from the docker library
FROM centos:7.7.1908
# Want the image completely patched. Have not tested without this.
RUN yum update -y

# Common tools. you can delete this line or modify it as you like... 
RUN yum install epel-release vim screen git -y


# Install python 3.6 and pip3, which is critical to connecting to TLS compliant UCS systems
# Patching up because that is just what I do.
RUN yum install python36 python36-pip -y
RUN pip3 install --upgrade pip

# Install XML / JSON Handling
RUN pip3 install lxml && pip3 install xmljson

# Install the ucsmsdk using the 2.7 version of pip.
RUN pip3 install ucsmsdk

#Install imcsdk using the 2.7 version of pip.
RUN pip3 install imcsdk

#Install Ansible with pip3 so we get ansible fully compatible with python 3.6
RUN pip3 install ansible

# I do not install ansible from the repo because it gets mapped to 2.7 and appears to be difficult to change.
