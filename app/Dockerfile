FROM tomcat:10.0-jdk16

RUN apt update -y && \
    apt install -y net-tools

COPY conf/ /usr/local/tomcat/conf/
COPY sample.war /usr/local/tomcat/webapps/

#CMD ["catalina.sh", "run"]
