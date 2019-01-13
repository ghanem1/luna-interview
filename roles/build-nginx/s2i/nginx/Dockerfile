FROM centos
RUN yum -y install epel-release
RUN yum -y install nginx
ADD ./proxy.conf /etc/nginx/conf.d/
ADD ./run.sh /root
EXPOSE 8000
CMD ["/root/run.sh"]
