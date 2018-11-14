flink的java开发  
pom.xml文件

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.sina.flink</groupId>
    <artifactId>flink1.6_demo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <flink.version>1.6.0</flink.version>
        <scope.type>compile</scope.type>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-java</artifactId>
            <version>${flink.version}</version>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-streaming-java_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-clients_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>

        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-connector-kafka-0.10_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>

        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-table_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>

        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-streaming-scala_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>

        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-scala_2.11</artifactId>
            <version>${flink.version}</version>
        </dependency>

        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.2</version>
        </dependency>



    </dependencies>

    <build>
    <plugins>
        <!-- Scala Compiler -->
        <plugin>
            <groupId>net.alchim31.maven</groupId>
            <artifactId>scala-maven-plugin</artifactId>
            <version>3.2.2</version>
            <executions>
                <!-- Run scala compiler in the process-resources phase, so that dependencies on
                  scala classes can be resolved later in the (Java) compile phase -->
                <execution>
                    <id>scala-compile-first</id>
                    <phase>process-resources</phase>
                    <goals>
                        <goal>compile</goal>
                    </goals>
                </execution>
                <execution>
                    <id>scala-test-compile</id>
                    <phase>process-test-resources</phase>
                    <goals>
                        <goal>testCompile</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <jvmArgs>
                    <jvmArg>-Xms128m</jvmArg>
                    <jvmArg>-Xmx512m</jvmArg>
                </jvmArgs>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.0.0</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <artifactSet>
                            <excludes>
                                <exclude>org.apache.flink:flink-annotations</exclude>
                                <exclude>org.apache.flink:flink-shaded-hadoop2</exclude>
                                <exclude>org.apache.flink:flink-shaded-curator-recipes
                                </exclude>
                                <exclude>org.apache.flink:flink-core</exclude>
                                <exclude>org.apache.flink:flink-java</exclude>
                                <exclude>org.apache.flink:flink-scala_2.11</exclude>
                                <exclude>org.apache.flink:flink-runtime_2.11</exclude>
                                <exclude>org.apache.flink:flink-optimizer_2.11</exclude>
                                <exclude>org.apache.flink:flink-clients_2.11</exclude>
                                <exclude>org.apache.flink:flink-avro_2.11</exclude>
                                <exclude>org.apache.flink:flink-examples-batch_2.11</exclude>
                                <exclude>org.apache.flink:flink-examples-streaming_2.11
                                </exclude>
                                <exclude>org.apache.flink:flink-streaming-java_2.11</exclude>
                                <exclude>org.apache.flink:flink-streaming-scala_2.11</exclude>
                                <exclude>org.apache.flink:flink-scala-shell_2.11</exclude>
                                <exclude>org.apache.flink:flink-python</exclude>
                                <exclude>org.apache.flink:flink-metrics-core</exclude>
                                <exclude>org.apache.flink:flink-metrics-jmx</exclude>
                                <exclude>org.apache.flink:flink-statebackend-rocksdb_2.11
                                </exclude>

                                <!-- Also exclude very big transitive dependencies of Flink

                                WARNING: You have to remove these excludes if your code relies on other
                                versions of these dependencies.
                                -->
                                <exclude>log4j:log4j</exclude>
                                <exclude>org.scala-lang:scala-library</exclude>
                                <exclude>org.scala-lang:scala-compiler</exclude>
                                <exclude>org.scala-lang:scala-reflect</exclude>
                                <exclude>com.data-artisans:flakka-actor_*</exclude>
                                <exclude>com.data-artisans:flakka-remote_*</exclude>
                                <exclude>com.data-artisans:flakka-slf4j_*</exclude>
                                <exclude>io.netty:netty-all</exclude>
                                <exclude>io.netty:netty</exclude>
                                <exclude>commons-fileupload:commons-fileupload</exclude>
                                <exclude>org.apache.avro:avro</exclude>
                                <exclude>commons-collections:commons-collections</exclude>
                                <exclude>com.thoughtworks.paranamer:paranamer</exclude>
                                <exclude>org.xerial.snappy:snappy-java</exclude>
                                <exclude>org.apache.commons:commons-compress</exclude>
                                <exclude>org.tukaani:xz</exclude>
                                <exclude>com.esotericsoftware.kryo:kryo</exclude>
                                <exclude>com.esotericsoftware.minlog:minlog</exclude>
                                <exclude>org.objenesis:objenesis</exclude>
                                <exclude>com.twitter:chill_*</exclude>
                                <exclude>com.twitter:chill-java</exclude>
                                <exclude>commons-lang:commons-lang</exclude>
                                <exclude>junit:junit</exclude>
                                <exclude>org.apache.commons:commons-lang3</exclude>
                                <exclude>org.slf4j:slf4j-api</exclude>
                                <exclude>org.slf4j:slf4j-log4j12</exclude>
                                <exclude>log4j:log4j</exclude>
                                <exclude>org.apache.commons:commons-math</exclude>
                                <exclude>org.apache.sling:org.apache.sling.commons.json
                                </exclude>
                                <exclude>commons-logging:commons-logging</exclude>
                                <exclude>commons-codec:commons-codec</exclude>
                                <exclude>com.fasterxml.jackson.core:jackson-core</exclude>
                                <exclude>com.fasterxml.jackson.core:jackson-databind</exclude>
                                <exclude>com.fasterxml.jackson.core:jackson-annotations
                                </exclude>
                                <exclude>stax:stax-api</exclude>
                                <exclude>com.typesafe:config</exclude>
                                <exclude>org.uncommons.maths:uncommons-maths</exclude>
                                <exclude>com.github.scopt:scopt_*</exclude>
                                <exclude>commons-io:commons-io</exclude>
                                <exclude>commons-cli:commons-cli</exclude>
                                <exclude>org.apache.hadoop:hadoop-client</exclude>
                                <exclude>org.apache.hadoop:hadoop-mapreduce-client-app
                                </exclude>
                                <exclude>org.apache.hadoop:hadoop-mapreduce-client-common
                                </exclude>
                                <exclude>org.apache.hadoop:hadoop-yarn-client</exclude>
                                <exclude>org.apache.hadoop:hadoop-yarn-server-common</exclude>
                                <exclude>org.apache.hadoop:hadoop-mapreduce-client-shuffle
                                </exclude>
                                <exclude>org.apache.hadoop:hadoop-mapreduce-client-core
                                </exclude>
                                <exclude>org.apache.hadoop:hadoop-yarn-common</exclude>
                                <exclude>org.apache.hadoop:hadoop-auth</exclude>

                                <exclude>org.apache.hadoop:hadoop-common</exclude>
                                <exclude>org.apache.hadoop:hadoop-annotations</exclude>

                                <exclude>org.apache.hadoop:hadoop-yarn-api</exclude>
                                <exclude>org.apache.hadoop:hadoop-mapreduce-client-jobclient
                                </exclude>
                                <exclude>org.apache.hadoop:hadoop-hdfs</exclude>
                                <exclude>io.netty:netty</exclude>
                                <exclude>com.google.protobuf:protobuf-java</exclude>
                                <exclude>com.google.code.findbugs:jsr305</exclude>
                                <exclude>org.slf4j:*</exclude>
                                <exclude>log4j:*</exclude>
                            </excludes>
                        </artifactSet>
                        <filters>
                            <filter>
                                <!-- Do not copy the signatures in the META-INF folder.
                                Otherwise, this might cause SecurityExceptions when using the JAR. -->
                                <artifact>*:*</artifact>
                                <excludes>
                                    <exclude>META-INF/*.SF</exclude>
                                    <exclude>META-INF/*.DSA</exclude>
                                    <exclude>META-INF/*.RSA</exclude>
                                </excludes>
                            </filter>
                        </filters>
                        <transformers>
                            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>my.programs.main.clazz</mainClass>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        <plugin>
            <!-- just define the Java version to be used for compiling and plugins -->
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.1</version><!--$NO-MVN-MAN-VER$-->
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <!-- The output of Xlint is not shown by default, but we activate it for the QA bot
                to be able to get more warnings -->
                <compilerArgument>-Xlint:all</compilerArgument>
            </configuration>
        </plugin>
    </plugins>
    </build>
</project>
```




启动脚本
```
flink14 run \
-m yarn-cluster \
-yn 7 \
-ys 1 \
-ynm flink_ods_bhv_tblog \
-yd -yD yarn.containers.vcores=1 \
-c main.ods_bhv_tblog_mian \
target/flink_ods_bhv_tblog-1.0-SNAPSHOT.jar
```

主类
```

```






















































































