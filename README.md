# Wildfly Spatial
Docker container containing Wildfly with Hibernate Spatial and MySQL / Postgres JDBC drivers

### Building the container
```sh
cd 10.0.0.Final && docker build -t wildfly-spatial:10.0.0.Final .
```

### Example run
To boot in standalone mode

```sh
docker run -it wildfly-spatial:10.0.0.Final
```

To boot in domain mode

```sh
docker run -it wildfly-spatial:10.0.0.Final /opt/jboss/wildfly/bin/domain.sh -b 0.0.0.0 -bmanagement 0.0.0.0
```
