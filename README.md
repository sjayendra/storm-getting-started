storm-getting-started
=====================

Installation
------------

0- You need to install Java, Leiningen or Maven for project management (optional, but recommended), and Git for pulling repositories (optional, but recommended).

1- Install Java. I am not sure there are any reliable deb repos for this for Ubuntu, so I downloaded from the JDK from Oracle's web site.

2- Install either Leiningen or Maven for project management.

Maven is a Java tool for downloading dependencies and running tasks on a project so that you don't need an IDE or custom compilation scripts. It requires a pom.xml file that declares the dependencies of a project. It is convention based, so that you don't need to specify the location of your source files; i.e. they need to be in a folder called source/main/java. The command to use Maven is mvn.

To install Maven, again either use the one in the repo (not recommended) or download manually and add the bin directory to your path.

    wget http://www.bizdirusa.com/mirrors/apache/maven/maven-3/3.0.4/binaries/apache-maven-3.0.4-bin.tar.gz
    tar xf apache-maven-3.0.4-bin.tar.gz
    export PATH=$PATH:/home/vagrant/apache-maven-3.0.4/bin

Leiningen is a tool that uses Maven internally for dependency management, but it is more suited for Clojure projects (Part of Storm was written in Clojure, a Lisp that runs on JVM, and there is a Clojure DSL for defining topologies. I suggest you to learn it and try to use it as it seems to be the project author's (Nathan Marz) choice too. Note that you *can* compile and run your Java project with Lein, it is not required that you write your code in Clojure to be able to use it.) The command to use Leiningen is lein.

Its installation is simpler, but Storm examples currently use an older Leiningen version, so beware. The latest version is 2.0, but you need to install 1.7.1 for the moment.

    mkdir -p ~/bin; cd ~/bin;
    wget https://raw.github.com/technomancy/leiningen/1.7.1/bin/lein
    chmod +x lein

Now, add the ~/bin directory on your PATH and execute the lein command. On first run, it will download the required libraries for its own use.

    lein

3- Install Git.

    sudo apt-get install git

4- Clone the `storm-starter' repository on Github.

    git clone https://github.com/nathanmarz/storm-starter.git

5- Follow the instructions at https://github.com/nathanmarz/storm-starter


   For Leiningen, to run a Java project:

    lein deps
    lein compile
    java -cp $(lein classpath) storm.starter.ExclamationTopology

To run a Clojure project,

    lein deps
    lein compile
    lein run -m storm.starter.clj.word-count

For Maven, to run a Java project,

    mvn -f m2-pom.xml compile exec:java -Dexec.classpathScope=compile -Dexec.mainClass=storm.starter.WordCountTopology

Note that instead of pom.xml here we forced Maven to use the m2-pom.xml file instead. In your own projects, you could simply rename this pom.xml and get rid of the `-f m2-pom.xml' section.
