# Maven Dependency Management Extension

A Maven core extension which allows additional dependency management features such as overriding a dependency version from the command line.

If any of the extension's options are used, they are recorded in .properties format in META-INF/maven/groupId/artifactId/, the same place that maven copies the normal pom file to. An "effective pom" representation of the post-modification model is written in the same directory as well. These actions help mitigate loss of build repeatability.

## Usage
Pass one or more properties to the maven build in the form:

    version:<groupId>:<artifactId>=<version>

to override **dependency versions**. Pass one or more properties to the maven build in the form:

    pluginVersion:<groupId>:<artifactId>=<version>

to override **plugin versions**.

It is possible to specify a remote POM for the purposes of affecting the plugin or dependency management instead of a series of properties. For dependencies, use:

    dependencyManagement=<groupId>:<artifactId>:<version>

and for plugins use:

    pluginManagement=<groupId>:<artifactId>:<version>

### Examples
The following overrides **junit**  to version **4.10**

    mvn install -Dversion:junit:junit=4.10

The following overrides **plexus-component-metadata**  to version **1.5.5**

    mvn install -DpluginVersion:org.codehaus.plexus:plexus-component-metadata=1.5.5

## Installation options
### Install from source
After cloning the repo, you can make the extension active for all maven builds by running the following commands:

    mvn package && sudo cp target/maven-dependency-management-extension*.jar /usr/share/maven/lib/ext/

### Install from Maven Central

The jar can be downloaded from Maven Central here (save to `/usr/share/maven/lib/ext/` or `$M2_HOME/lib/ext`): http://repo1.maven.org/maven2/org/jboss/maven/extension/dependency/maven-dependency-management-extension/

### Activate for an individual project
Add this to **pom.xml** (fill in **VERSION**, eg 1.0.1):

    <build>
        <extensions>
            <extension>
                <groupId>org.jboss.maven.extension.dependency</groupId>
                <artifactId>maven-dependency-management-extension</artifactId>
                <version>VERSION</version>
            </extension>
        </extensions>
    </build>

## Uninstall
If you wish to remove the extension after installing it, run the following command:

    sudo rm -i /usr/share/maven/lib/ext/maven-dependency-management-extension*.jar

## Run Integration Tests
The following command runs the integration tests as part of the build

    mvn install -Prun-its

