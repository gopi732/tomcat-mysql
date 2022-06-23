FROM tomcat:9-jdk8
LABEL author="gopi"
RUN mv webapps webapps2 && mv webapps.dist/ webapps
COPY gameoflife.war /usr/local/tomcat/webapps/gameoflife.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
