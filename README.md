Pega Docker Image
===========

This project is a slim version of pega-web docker image that runs pega application expecting prweb.war to be mounted while performing docker run.  


# Build

Docker (you may replace pega-tomcat with the name you wish to give the resulting image):

`docker build -t pega-tomcat .`


# Run

**Mounting Options of prweb**

1. Mount from host machine to `/usr/local/tomcat/webapps` in docker container using `-v argument` in `docker run` command

```bash
$ docker run -v /some/local/directory/prweb.war:/usr/local/tomcat/webapps/prweb.war:z <image name>
```

2. Provide the URL where your prweb.war is located as an argument in `docker run` command


```bash
$ docker run -e PRWEB_URL="http://<hostname>" <image name>
```

**Using environment variables**

You can make adjustments by overriding environmental variables
```bash
$ docker run -e "DB_HOST=55.55.55.1" -e "DB_PORT=1234" <image name>[:tags]
```

You can provide a directory containing a `prconfig.xml` and `prlog4j2.xml` file like so:

```bash
$ docker run -v /some/local/directory:/config <image name>:<build#>
```

Kafka data is saved to `/kafkadata` in the docker container. To persist the data, create a volume and mount it

## Environmental variables

**JDBC Driver**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| JDBC_DRIVER_URI              |                                  | https://jdbc.postgresql.org/download/postgresql-42.1.1.jre7.jar |
| JDBC_DRIVER_URI_USERNAME     |                                  |                |
| JDBC_DRIVER_URI_PASSWORD     |                                  |                |


**Global database variables**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| DB_USERNAME                  |                                  | postgres       |
| DB_PASSWORD | | postgres |
| DB_HOST | | localhost |
| DB_PORT | | 5432 |
| DB_NAME | | postgres |

**JDBC connection string**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| JDBC_CLASS | | org.postgresql.Driver |
| JDBC_DB_TYPE | | postgresql  |
| JDBC_URL_PREFIX | | //  |
| JDBC_URL_SUFFIX | |  |
| JDBC_MIN_ACTIVE | | 50  |
| JDBC_MAX_ACTIVE | | 250 |
| JDBC_MIN_IDLE | | 10 |
| JDBC_MAX_IDLE | | 50 |
| JDBC_MAX_WAIT | | 30000 |
| JDBC_INITIAL_SIZE | | 50 |
| JDBC_VALIDATION_QUERY | | SELECT 1 |

**Rule & data schema**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| RULES_SCHEMA | | rules |
| DATA_SCHEMA | | data |

**prweb URL**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| PRWEB_URL | Location where prweb.war is hosted | |


**Customize the tomcat runtime**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| MAX_THREADS | | 300 |
| JAVA_OPTS | | |
| INITIAL_HEAP | | 2048m |
| MAX_HEAP | | 4096m |
| INDEX_DIRECTORY | | NONE |
| HEAP_DUMP_PATH | | /heapdumps |
| NODE_ID | | "NONE" |
| CONFIG_DIRECTORY | | /config |

**Remote JMX support**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| JMX_PORT | | 9001 |
| JMX_SERVER_HOSTNAME | | 127.0.0.1 |
| TOMCAT_JMX_JAR_TGZ_URL | | https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/extras/catalina-jmx-remote.jar |

**DDS/Cassandra settings**

|  Name                        | Purpose                          | Default        |
| ---------------------------- | -------------------------------- | -------------- |
| CASSANDRA_CLUSTER | whether to enable external cassandra | false |
| CASSANDRA_NODES | comma separated list of nodes (e.g. `10.20.205.26,10.20.205.233`) | |
| CASSANDRA_PORT | cql port | 9042 |
| CASSANDRA_USERNAME | username | dnode_ext |
| CASSANDRA_PASSWORD | password | dnode_ext |
