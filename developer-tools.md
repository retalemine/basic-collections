####Development Kits:
* JDK 8
  * sudo update-alternatives --config java
  * JAVA_HOME=/opt/jdk1.8.0_31
  * JRE_HOME=/opt/jdk1.8.0_31/jre
  * PATH=$PATH:$JAVA_HOME/bin
  * export JAVA_HOME
  * export JRE_HOME
  * export PATH
  * sudo update-alternatives --install "/usr/bin/[java|javac|javaws]" "[java|javac|javaws]" "/usr/local/java/jdk1.8.0_20/bin/[java|javac|javaws]" 1
  * sudo update-alternatives --set [java|javac|javaws] /usr/local/java/jdk1.8.0_20/bin/[java|javac|javaws]

####IDE:
* Eclipse 
  * MaxPermSize=512m
  * Xmx1024m

####Project Management Tools:
* Maven
  * export PATH=$PATH:/opt/apache-maven-3.2.5
  * export MAVEN_OPTS="-Xms256m -Xmx512m"

####GIT:
* git clone --depth 1 [git-url]

####Debian manipulation:
```
mkdir deb$$
cp <pkg>.deb deb$$
cd deb$$
dpkg-deb -x <pkg>.deb deb
cd deb
dpkg-deb -e ../<pkg>.deb
nano DEBIAN/control
replace the old dependecy to newer version 
or 
remove the dependecy and add the so file in appropriate folder
cp /usr/share/..libxx.so.xx deb/opt/...
cd ..
sudo dpkg-deb -b debian-installer
```
