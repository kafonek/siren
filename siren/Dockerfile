FROM sirensolutions/siren-platform-demo-data

### Install mysql for connections to relational.fit.cvut.cz
WORKDIR /tmp
RUN wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java_8.0.25-1debian10_all.deb \
    && dpkg-deb -x mysql-connector-java_8.0.25-1debian10_all.deb /tmp/connector \
    && cp /tmp/connector/usr/share/java/mysql-connector-java-8.0.25.jar /opt/platform/elasticsearch/config/jdbc-drivers


WORKDIR /