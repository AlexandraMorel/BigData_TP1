# Crevisier - Morel assignment

## Bash command

### Maven on local machine:
```
        mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=org.bigdata.tp1_2 -DartifactId=BankingAccount -DinteractiveMode=false
        cd ./Users/alexandra/BankingAccount
        mvn eclipse:eclipse
```

Add to POM.xml:
```xml
        <dependency>
                <groupId>org.apache.hadoop</groupId>
                <artifactId>hadoop-core</artifactId>
                <version>1.2.1</version>
        </dependency>
```

Then re-run
```
        mvn eclipse:eclipse
        mvn jar:jar
```

> Same commands for FriendsMean

### Git Bash:
```
        scp ./Users/alexandra/BankingAccount/target/BankingAccount-1.0-SNAPSHOT.jar amorel@hadoop-ece.tk:/home/amorel/BigDataTP1 
        scp ./Users/alexandra/FriendsMean/target/FriendsMean-1.0-SNAPSHOT.jar amorel@hadoop-ece.tk:/home/amorel/BigDataTP1 
        ssh amorel@hadoop-ece.tk
        mkdir ./BigDataTP1
        cd ./BigDataTP1
        git init
        vim README.md
        vim AUTHORS
        git add README.md
        git add AUTHORS
        git commit -m "Add AUTHORS and README.md files"
        git add BankingAccount-1.0-SNAPSHOT.jar
        git add FriendsMean-1.0-SNAPSHOT.jar
        git commit -m "Add .jar"
```
We initialize a kerboros ticket and launch the jar file.
```
        kinit
        export JAVA_HOME=/usr/java/default
        export PATH=${JAVA_HOME}/bin:${PATH}
        export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
        hadoop jar BankingAccount-1.0-SNAPSHOT.jar org.bigdata.tp1_2.BankAccount /res/mapred_assignment /home/amorel/output
```
When we launch that, we don't have any result. 
```
15/11/01 20:25:43 INFO mapreduce.Job:  map 0% reduce 0%
```
We can't understand why so we can't provide any result.

Problem when we try to put files of the git on the Github: 
```
        git remote add origin git@github.com:AlexandraMorel/BigDataTP1.git
        git push origin master
```
We obtain "Permission denied (publickey)." so we create a SSH key to identify our local machine as a trusted computer.
```
        ssh-keygen -t rsa -b 4096 -C "amorel@edu.ece.fr"
        eval $(ssh-agent -s)
        ssh-add ~/.ssh/id_rsa
        clip < ~/.ssh/id_rsa.pub
```
We add .jar for each exercises.
```
        git add ./BankingAccount-1.0-SNAPSHOT.jar
        git commit -m "add bankingaccount files"
        git push --set-upstream git@github.com:AlexandraMorel/BigData_TP1.git master
        git pull git@github.com:AlexandraMorel/BigData_TP1.git
        git add ./FriendsMean-1.0-SNAPSHOT.jar
        git commit -m "add friendsmean files"
        git push --set-upstream git@github.com:AlexandraMorel/BigData_TP1.git master
        git pull git@github.com:AlexandraMorel/BigData_TP1.git
```

#### II. Practice 1
Question
> It is useful to use the Reducer Class as a Combiner because it's an addition function (it would not be useful for a mean function). It can be used because the function is both commutative and associative.
