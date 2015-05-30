# Simple Drill Examples
This project contains examples of user defined functions for Apache Drill.  

These are packaged as a separate project so that you can clone this project as a head start in creating your own 
extensions for Drill.

## How to Compile Install
Clone this package and compile it.

    git clone https://github.com/mapr-demos/simple-drill-functions.git
    cd simple-drill-functions
    mvn package
    cd ..
    
Now download and unpack Apache Drill. 

    wget http://getdrill.org/drill/download/apache-drill-1.0.0.tar.gz
    tar xvf apache-drill-1.0.0.tar.gz

Copy the jar files from your functions into the 3rdparty directory in the Drill distro

    cp simple-drill-functions/target/*.jar apache-drill-1.0.0/jars/3rdparty

Edit the `drill-override.conf` file to add a reference to the package these functions live in:

    echo 'drill.logical.function.package+=[com.mapr.drill]' >> apache-drill-1.0.0/conf/drill-override.conf

Now run drill and test the results

    $ cd apache-drill-1.0.0/
    $ bin/drill-embedded
    0: jdbc:drill:zk=local> select myaddints(position_id, 3) from cp.`employee.json` limit 3;
    +---------+
    | EXPR$0  |
    +---------+
    | 4.0     |
    | 5.0     |
    | 5.0     |
    +---------+