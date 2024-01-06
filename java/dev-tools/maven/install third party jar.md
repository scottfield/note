#Guide to installing 3rd party JARs
Although rarely, but sometimes you will have 3rd party JARs that you need to put in your local repository for use in your builds, since they don't exist in any public repository like Maven Central. The JARs must be placed in the local repository in the correct place in order for it to be correctly picked up by Apache Maven. To make this easier, and less error prone, we have provide a goal in the maven-install-plugin which should make this relatively painless. To install a JAR in the local repository use the following command:
```
mvn install:install-file -Dfile=<path-to-file>-DgroupId=<group-id> \
-DartifactId=<artifact-id>-Dversion=<version>-Dpackaging=<packaging>
```
If there's a pom-file as well, you can install it with the following command:
```
mvn install:install-file -Dfile=<path-to-file>-DpomFile=<path-to-pomfile>
```
With version 2.5 of the maven-install-plugin it gets even better. If the JAR was built by Apache Maven, it'll contain a pom.xml in a subfolder of the META-INF directory, which will be read by default. In that case, all you need to do is:
```
mvn install:install-file -Dfile=<path-to-file>
```
Javadoc and sources are just artifacts with a classifier of the same pom.
For example:
Install the main artifact
```
mvn install:install-file -Dfile=matlabcontrol-4.1.0.jar-DgroupId=matlab -DartifactId=matlab -Dversion=4.1.0
```
Install the javadoc using the classifier javadoc:
```
mvn install:install-file -Dfile=matlabcontrol-4.1.0.jar-DgroupId=matlab -DartifactId=matlab -Dversion=4.1.0-Dclassifier=javadoc
mvn install:install-file --offline -s "D:\Program Files\apache-maven-3.3.9\conf\settings.xml" -Dmaven.repo.local=D:\repository  -Dfile=D:\iijdbc.jar -DgroupId=com.synnex.hyve -DartifactId=vector-db-driver -Dversion=1.0 -Dpackaging=jar
```