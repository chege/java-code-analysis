PDM Rule sets
============
A collection of rules to be executed in a PMD run.

How to include in Maven
-----------------------
Include this in the pom.xml file's `pluginManagement` element or in
`plugins` element if the project doesn't use the plugin management. If
plugin management is not used, this will activate the plugin and the 
next step is not needed.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-pmd-plugin</artifactId>
  <version>3.12.0</version>
  <configuration>
    <compileSourceRoots>
      <sourceRoot>${basedir}/src/main/java/</sourceRoot>
      <sourceRoot>${basedir}/src/test/java/</sourceRoot>
    </compileSourceRoots>
    <rulesets>
      <ruleset>pmd-ruleset.xml</ruleset>
    </rulesets>
    <printFailingErrors>true</printFailingErrors>
    <linkXRef>false</linkXRef>
     <!-- Add this if you want to exclude files -->
     <excludeFromFailureFile>exclude-pmd.properties</excludeFromFailureFile>
  </configuration>
  <executions>
    <execution>
      <goals>
        <goal>check</goal>
      </goals>
    </execution>
  </executions>
  <dependencies>
    <dependency>
      <groupId>io.github.chege.javacodeanalysis</groupId>
      <artifactId>pmd-rulesets</artifactId>
      <version>1.0-SNAPSHOT</version>
    </dependency>
  </dependencies>
</plugin>
```



If you do use plugin management, include this in the pom.xml file's 
`plugins` element to activate the plugin.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-pmd-plugin</artifactId>
</plugin>
```

How to exclude files from being scanned
------------------------------
There are times where PMD reports false negatives and therefore exclusion of files is needed.

1. Create a properties file, e.g. `exclude-pmd.properties`, in the same folder as the `pom.xml` that configures the plugin is located – typically in the root of your maven project.
2. Add `excludeFromFailureFile` element to the configuration element of the PMD plugin

### Example 

```xml
  ...
  <excludeFromFailureFile>exclude-pmd.properties</excludeFromFailureFile>
</configuration>
```

`exclude-pmd.properties`
```properties
io.github.chege.springdemo.UserController=UnusedPrivateField
```

