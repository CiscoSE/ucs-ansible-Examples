Two docker files are provided for creating Docker containers for use with the Ansible examples provided in this repository. 

1)  7.6/Dockerfile creates a docker container based on CentOS 7.6.
2)  8.0/Dockerfile creates a docker container based on CentOS 8.0

The latest ucssdk, and the latest imcsdk will be installed via PIP. The latest version of Ansible is also installed with PIP3.

From either folder, run the following command to make a docker container with Ansible configured for UCS:

> docker build -t ansble/ucs:latest .


