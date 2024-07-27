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
  * tar -xvf eclipse-jee-2020-12-R-linux-gtk-x86_64.tar.gz -C /myopt/programfiles/eclipse
* Visual Studio Code

####Project Management Tools:
* Maven
  * export PATH=$PATH:/opt/apache-maven-3.2.5
  * export MAVEN_OPTS="-Xms256m -Xmx512m"
* Gradle
  * unzip -d /myopt/programfiles/gradle gradle-6.8-bin.zip

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

####Tool Manager
* https://sdkman.io/install

####Web Tools
* nodejs
  * tar -xvf node-v14.15.4-linux-x64.tar.xz -C /myopt/programfiles/nodejs


NODSJS_HOME= D:\NodeJS.V.0.12.0
NODEJS_MODULES= D:\NodeJS.V.0.12.0\node_modules
NODEJS_NPM= D:\NodeJS.V.0.12.0\node_modules\npm

npm install electron --save-dev [--save-exact]
npm install -g electron@latest

* a microservices-based system would be ideal for a reporting system on a company’s retail store sales. Each step in the data preparation process would be handled by a microservice: data collection, cleansing, normalization, enrichment, aggregation, reporting, etc. 
* An microservices-based ML environment collects, aggregates, and analyzes a data flow so that the ML framework can determine an outcome.
* ML frameworks - TensorFlow, Apache Mahout, and Apache Singa.
* You use a framework by calling its methods, inheriting its classes, implementing its interfaces, and by supplying callbacks, listeners, and other software constructs. 

####Software Architecture Questions
Is the software primarily client software, server software, or both?
Are you creating a new application or adding functionality to an existing application?
Will you deploy a standalone application, deploy your application in an application server like JBoss, or deploy your application as a small independent service?
What language and technologies are familiar to you and your team?
Are there any accepted industry standards should your software implement?
Will you deploy the software in the cloud, for example, as an Amazon Web Services (AWS) Lambda function?

health checks, metrics, tracing and fault tolerance, and integrate with Prometheus, Jaeger/Zipkin and Kubernetes.
Apache Kafka, any AMQP, RabbitMQ, ActiveMQ
Consul, Prometheus, Jaeger, Grafana
Docker, Kubernetes, OpenTracing, Etcd, DevOps
Catching support, Load Balancing, Clustering
Mocking, Profiling

OPENJDK
MICROPROFILE
NETTY
JERSEY
OPENTRACING
OPENAPI
GRAALVM
PROMETHEUS
JAEGER
ZIPKIN
DOCKER
KUBERNETES

IDE	Eclipse with node.js plugins, Jetbrains Webstorm, Cloud9 IDE,
Visual Studio Node JS Toolkit
Database	Mongoose for MongoDB
UI Build Tools	Grunt, Yeoman, Gulp
CLI	Node CLI, grunt-cli
Authentication	Passport.js
UI Library Management	Bower
UI Frameworks	Backbone.js, Angular.js, Ember.js
Layout Frameworks	Twitter Bootstrap Framework
Template Engine	Jade, EJS, Hogan.JS
CSS Engine	Stylus, LESS, Compass
Unit Testing Frameworks	Jasmin, Node Unit
