# maven-release-plugin-example


### Cleaning a Release

1. Delete the release descriptor (release.properties)

2. Delete any backup POM files

```
mvn release:clean
```



### Preparing the Release

1. Perform some checks – there should be no uncommitted changes and the project should depend on no SNAPSHOT dependencies

2. Change the version of the project in the pom file to a full release number (remove SNAPSHOT suffix) – in our example – 0.1

3. Run the project test suites

4. Commit and push the changes

5. Create the tag out of this non-SNAPSHOT versioned code

6. Increase the version of the project in the pom – in our example – 0.2-SNAPSHOT

7. Commit and push the changes


### Dry Run

Allows you to run all operations in `release:prepare` goal except for actual commits into SCM.

```
mvn release:prepare -DdryRun=true
```


### Performing the Release

1. Checkout release tag from SCM

2. Build and deploy released code

3. Relies on the output of the Prepare step – the `release.properties`.


```
mvn release:prepare
```

### Hosted Maven2 repository in Nexus

Create maven2 hosted repository in Nexus, for us it's `api-release`


### Upload artifact in Nexus from command line:

```
curl -v --user admin:admin123 --upload-file <filename> http://localhost:8081/repository/<repository-name>/<filename>
```


### Configure the credentials for the nexus-releases server in the global `settings.xml` (%USER_HOME%/.m2/settings.xml):


```
<servers>
   <server>
      <id>nexus-releases</id>
      <username>admin</username>
      <password>admin123</password>
   </server>
</servers>
```

### Cleaning, Preparing and Performing the release


```
mvn release:clean release:prepare release:perform -DreleaseVersion=0.1 -DdevelopmentVersion=0.2-SNAPSHOT
```

Reference: http://www.baeldung.com/maven-release-nexus
