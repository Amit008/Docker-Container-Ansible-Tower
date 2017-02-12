# Docker-Container-Ansible-Tower 3.0.3

Was Trying out to Build Docker Container For Ansible Tower on Centos

To build this container have to make centos work with systemd which is a requirement to run ansible tower.

Centos is now providing Centos 7 image with Systemd which can be downloaded from docker hub

This is not a offical Docker container from Ansible and this is only meant for learning purpose how we can build Ansible Tower Container using docker.


Setting Up Docker Container for Ansible-tower is 2 step process:
1.Building Ansible Tower Image based on Centos systemd image which is referenced in Dockerfile.

Build the docker container:
docker build -t ansible-tower .

2.After sucessfully building docker ansible image create docker container using this image.

 docker run -h ansible -it --rm --security-opt seccomp=unconfined --stop-signal=SIGRTMIN+3 --tmpfs /run --tmpfs /run/lock -v tower:rw -v ~/PlugVolume/awx/main:/var/lib/awx:rw -v ~/PlugVolume/awx/log:/var/log/tower:rw -v /sys/fs/cgroup:/sys/fs/cgroup:ro -v ~/Docker/ansible/ansible-tower-setup-3.0.3/:/tmp/tower:rw -p 8080 -p 443 <Docker Image id>


in this command two volumes are mounted one for data and one for readonly system volume for systemd.

3. login to shell on docker container and execute the $Ansible_Setup_Home/setup.sh to finsh the configuration.

after sucessful installation you can login to ansible WebUI https://localhost:<portno>

to find the port 443 exposed on HostMachine you can use docker ps command to check the running container.


