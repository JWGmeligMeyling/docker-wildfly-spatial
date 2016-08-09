# vim:set ft=dockerfile:
FROM jboss/wildfly:10.0.0.Final
MAINTAINER Jan-Willem Gmelig Meyling <jan-willem@meylingmedia.nl>

RUN curl http://central.maven.org/maven2/org/hibernate/hibernate-spatial/5.0.7.Final/hibernate-spatial-5.0.7.Final.jar \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/hibernate-spatial-5.0.7.Final.jar \
	&& curl http://central.maven.org/maven2/com/vividsolutions/jts/1.13/jts-1.13.jar  \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/jts-1.13.jar \
	&& curl http://central.maven.org/maven2/org/geolatte/geolatte-geom/1.0.1/geolatte-geom-1.0.1.jar \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/geolatte-geom-1.0.1.jar \
	&& mkdir -p $JBOSS_HOME/modules/com/mysql/main \
	&& curl http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.39/mysql-connector-java-5.1.39.jar \
		-o $JBOSS_HOME/modules/com/mysql/main/mysql-connector-java-5.1.39-bin.jar \
	&& mkdir -p $JBOSS_HOME/modules/org/postgresql/main \
	&& curl http://central.maven.org/maven2/org/postgresql/postgresql/9.4-1206-jdbc42/postgresql-9.4-1206-jdbc42.jar \
		-o $JBOSS_HOME/modules/org/postgresql/main/postgresql-9.4-1206-jdbc42.jar

COPY ./mysql.module.xml /opt/jboss/wildfly/modules/com/mysql/main/module.xml
COPY ./postgres.module.xml /opt/jboss/wildfly/modules/org/postgresql/main/module.xml
COPY ./hibernate.module.xml /opt/jboss/wildfly/modules/system/layers/base/org/hibernate/main/module.xml
COPY ./standalone.xml /opt/jboss/wildfly/standalone/configuration/standalone.xml

EXPOSE 9990

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
