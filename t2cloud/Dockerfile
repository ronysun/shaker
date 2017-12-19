FROM centos:centos7.3.1611

MAINTAINER sunluning  <sunluning@t2cloud.net
ENV repo_ip 192.168.102.20
ENV version 2.2.4
RUN echo -e '[openstack_http]\nbaseurl=http://192.168.102.20:10088/\nenabled=1\ngpgcheck=0\nname=cloud repository' > /etc/yum.repos.d/openstack_http.repo
RUN yum -y install python-pip gcc python-devel libffi-devel openssl-devel gcc-c++
RUN pip install pyshaker
RUN pip uninstall -y python-keystoneclient python-novaclient python-neutronclient \
        python-glanceclient python-heatclient
RUN pip install python-keystoneclient==$version.* \
                python-novaclient==$version.* \
                python-neutronclient==$version.* \
                python-cinderclient==$version.* \
                python-glanceclient==$version.* \
                python-cloudkittyclient==$version.* \
                python-heatclient==$version.* \
                -i http://$repo_ip:10087/simple/ --trusted-host $repo_ip
WORKDIR /home/ 
