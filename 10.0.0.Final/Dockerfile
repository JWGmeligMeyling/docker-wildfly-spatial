# vim:set ft=dockerfile:
FROM jboss/wildfly:10.0.0.Final
MAINTAINER Jan-Willem Gmelig Meyling <jan-willem@meylingmedia.nl>

ENV SERVER_CLI /opt/jboss/wildfly/bin/jboss-cli.sh

RUN curl http://central.maven.org/maven2/org/hibernate/hibernate-spatial/5.0.7.Final/hibernate-spatial-5.0.7.Final.jar \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/hibernate-spatial-5.0.7.Final.jar \
	&& curl http://central.maven.org/maven2/com/vividsolutions/jts/1.13/jts-1.13.jar  \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/jts-1.13.jar \
	&& curl http://central.maven.org/maven2/org/geolatte/geolatte-geom/1.0.1/geolatte-geom-1.0.1.jar \
		-o $JBOSS_HOME/modules/system/layers/base/org/hibernate/main/geolatte-geom-1.0.1.jar \
	&& curl http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.39/mysql-connector-java-5.1.39.jar \
		-o mysql-connector-java-5.1.39-bin.jar \
	&& /opt/jboss/wildfly/bin/jboss-cli.sh --connect "module add --name=com.mysql.jdbc.Driver -resources=mysql-connector-java-5.1.39-bin.jar --dependencies=javax.api,javax.transaction.api" \
	&& /opt/jboss/wildfly/bin/jboss-cli.sh --connect "/subsystem=datasources/jdbc-driver=mysql:add(driver-name=mysql,driver-module-name=com.mysql.jdbc.Driver)" \
	&& curl http://central.maven.org/maven2/org/postgresql/postgresql/9.4-1206-jdbc42/postgresql-9.4-1206-jdbc42.jar \
		-o postgresql-9.4-1206-jdbc42.jar \
	&& /opt/jboss/wildfly/bin/jboss-cli.sh --connect "module add --name=org.postgresql.Driver --resources=postgresql-9.4-1206-jdbc42.jar --dependencies=javax.api,javax.transaction.api" \
	&& /opt/jboss/wildfly/bin/jboss-cli.sh --connect "/subsystem=datasources/jdbc-driver=postgres:add(driver-name=postgres,driver-module-name=org.postgresql.Driver)"

COPY ./hibernate.module.xml /opt/jboss/wildfly/modules/system/layers/base/org/hibernate/main/module.xml

EXPOSE 9990
