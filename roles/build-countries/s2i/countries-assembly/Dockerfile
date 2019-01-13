FROM centos
RUN yum -y install java-1.8.0-openjdk  java-1.8.0-openjdk-devel
ADD ./countries-assembly-1.0.1.jar /root/
CMD ["java","-jar","/root/countries-assembly-1.0.1.jar"]
