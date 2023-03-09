FROM centos
WORKDIR /mnt/p1
ENV Velocity AWS
RUN cd /etc/yum.repos.d/
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
RUN yum update -y && yum install git vim  maven wget unzip -y 
RUN yum install -y \
       java-1.8.0-openjdk \
       java-1.8.0-openjdk-devel
ENV JAVA_HOME /etc/alternatives/jre
RUN  mkdir /mnt/servers/ && cd /mnt/servers/ && wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.73/bin/apache-tomcat-9.0.73.zip && unzip apache-tomcat-9.0.73.zip
RUN chmod -R 777  /mnt/servers/apache-tomcat-9.0.73/bin/*
RUN git clone https://github.com/akshay00000/game-of-life.git
RUN cd /mnt/p1/game-of-life &&  mvn clean install
EXPOSE 8080
RUN cp /mnt/p1/game-of-life/gameoflife-web/target/gameoflife.war /mnt/servers/apache-tomcat-9.0.73/webapps/
MAINTAINER Nishant nishantshete5050@gmail.com

CMD ["/mnt/servers/apache-tomcat-9.0.73/bin/catalina.sh", "run"]

