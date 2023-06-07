FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe

RUN apt-get update && apt-get install -y tzdata
RUN apt-get update
RUN apt-get install -y iputils-ping
RUN apt-get install -y python3 python3-pip 
RUN apt-get install -y ansible
RUN apt-add-repository -y ppa:ansible/ansible
RUN apt-get update
RUN apt-get upgrade -y
RUN echo '[privilege_escalation]
      become_ask_pass = True 
      ' >> /etc/ansible/ansible.cfg
