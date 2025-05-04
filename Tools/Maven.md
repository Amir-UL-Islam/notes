```bash
find ~/.m2  -name "*.lastUpdated" -exec grep -q "Could not transfer" {} \; -print -exec rm {} \;
```
For removing cached in the local repository


For getting older version of maven
https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.2.1/

