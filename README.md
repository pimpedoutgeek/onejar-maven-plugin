# onejar-maven-plugin
Automatically exported from code.google.com/p/onejar-maven-plugin

Technique A - In addition to a 'regular' executable jar file

Just drop the following code into your pom.xml and run mvn package


<project>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>com.mycompany.mypackage.MyMainClass</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.dstovall</groupId>
                <artifactId>onejar-maven-plugin</artifactId>
                <version>1.4.4</version>
                <executions>
                    <execution>
                        <configuration>
                            <!-- Optional -->
                            <onejarVersion>0.97</onejarVersion>
                            <!-- Optional, use only if you need to include native libraries (dll's) -->
                            <binlibs>
                                <fileSet>
                                    <directory>${project.build.directory}/dllextract</directory>
                                    <includes>
                                        <include>test.dll</include>
                                    </includes>
                                </fileSet>
                            </binlibs>
                            <!-- Optional, default is false -->
                            <attachToBuild>true</attachToBuild>
                            <!-- Optional, default is "onejar" -->
                            <classifier>onejar</classifier>
                        </configuration>
                        <goals>
                            <goal>one-jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <pluginRepositories>
        <pluginRepository>
            <id>onejar-maven-plugin.googlecode.com</id>
            <url>http://onejar-maven-plugin.googlecode.com/svn/mavenrepo</url>
        </pluginRepository>
    </pluginRepositories>

</project>
Caveat

I wanted to get the latest version of this plugin out, and as a result I haven't spend the time to remove the warning from OneJar about a missing main/main.jar when this technique is used. I will be fixing this in the future, just not right now.

It (apparently) does not effect exectution and is just a warning.

The full text of the error is:

Boot: Warning: Unable to locate main/main.jar in the JAR file target/myproject-1.0-SNAPSHOT.one-jar.jar
Technique B - Instead of a 'regular' executable jar file

Just drop the following code into your pom.xml and run mvn package

<project>

    <build>
        <plugins>
            <plugin>
                <groupId>org.dstovall</groupId>
                <artifactId>onejar-maven-plugin</artifactId>
                <version>1.4.4</version>
                <executions>
                    <execution>
                        <configuration>
                            <mainClass>com.mycompany.mypackage.MyMainClass</mainClass>
                            <!-- Optional -->
                            <onejarVersion>0.97</onejarVersion>
                            <!-- Optional, use only if you need to include native libraries (dll's) -->
                            <binlibs>
                                <fileSet>
                                    <directory>${project.build.directory}/dllextract</directory>
                                    <includes>
                                        <include>test.dll</include>
                                    </includes>
                                </fileSet>
                            </binlibs>
                            <!-- Optional, default is false -->
                            <attachToBuild>true</attachToBuild>
                            <!-- Optional, default is "onejar" -->
                            <classifier>onejar</classifier>
                        </configuration>
                        <goals>
                            <goal>one-jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <pluginRepositories>
        <pluginRepository>
            <id>onejar-maven-plugin.googlecode.com</id>
            <url>http://onejar-maven-plugin.googlecode.com/svn/mavenrepo</url>
        </pluginRepository>
    </pluginRepositories>

</project>
