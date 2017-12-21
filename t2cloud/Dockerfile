FROM centos:centos7.3.1611

MAINTAINER sunluning  <sunluning@t2cloud.net>
ENV repo_ip 192.168.102.20
ENV version 2.2.4
ADD example_rc.sh /home/
ADD t2cloud /home/t2cloud
RUN echo -e '[openstack_http]\nbaseurl=http://192.168.102.20:10088/\nenabled=1\ngpgcheck=0\nname=cloud repository' > /etc/yum.repos.d/openstack_http.repo
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
RUN yum -y install python-pip gcc python-devel libffi-devel openssl-devel gcc-c++ screen openssh-server
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key && mkdir -p /var/run/sshd && echo "root:123456" | chpasswd 
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
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]
