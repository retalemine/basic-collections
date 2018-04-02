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
  * update-alternatives --display javac
  * update-alternatives --list javac
  * update-alternatives --config javac

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

####Setting Env Variables or Aliases
* ~/.profile
```
# set PATH so it includes maven bin if it exists
if [ -d "/opt/programfiles/apache-maven-3.3.9/bin" ] ; then
    PATH="/opt/programfiles/apache-maven-3.3.9/bin:$PATH"
fi
```
* ~/.bash_aliases
* LD_LIBRARY_PATH
  * sudo gedit /etc/ld.so.conf.d/randomLibs.conf
    * /home/linux/myLocalLibs
* printenv, ldconfig

####Arch
* For 32-bit Intel/AMD (x86) - i386 (i386, i686)
* For 64-bit Intel/AMD (x86_64) - amd64
* i386/AMD64/ARMv6/ARMv7

####Adding Debian repository link and public key for apt-secure
* Add to /etc/apt/sources.list	_note the distribution name_
```
deb http://download.virtualbox.org/virtualbox/debian vivid contrib
```
* Add the downloaded public key
```
sudo apt-key add oracle_vbox.asc
```
```
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O - | sudo apt-key add -
```
* sudo apt-get update
* sudo apt-get install virtualbox-5.0
