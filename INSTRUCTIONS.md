## Preparation

* Add the git lol command to your Git install with the following command:
  * git config --global --add alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit --all"
* Git Quick Tutorial for those who need it: https://try.github.io


## Project instructions

This project will assume that the group of students involved is composed of two or three students named A, B and C. If there are only two students in your group, the tasks of the student C will be realized by the student A or B depending on the student reviewing the work of the student C (if the student A is supposed to review the work of the student C, then the student B will do the work of the student C).

**You will have to follow VERY CAREFULLY all the instructions of this document.**

Each student is responsible of his/her task that includes the review of the code contributed by other members of your team. If somebody makes an error, you should detect it and prevent it during a code review. If the error is contributed in the project, then it the fault of the creator of the error **AND** the reviewer.

### Preparation

Each of the student must have an account on Github linked to their real name for me to grade your work. If you don't want to attach your real name to your Github account, send me an email indicating your name and Github account. All the steps in this project can be completed with a regular text editor and a terminal. If you want to use an IDE, you may have to add the maven support in your IDE and other things. Since it is not the goal of the project, **I will not handle IDE-related issues**.

### Creation of the organization and repositories

Create a Github organization with a **SIMPLE YET UNIQUE NAME** (preferably in lower case) and inside of this organization, fork the repository located at the URL https://github.com/sbegaudeau/alma-m2-2017. Then each of the student of your group should fork the repository at the URL https://github.com/ORGANIZATION_NAME/alma-m2-2017 in their own Github account. Each student should clone his/her own Git repository from Github on his/her machine. You will **always** work on your own local copy of your Git reposotiry. All the students of the group should be members of the Git repository of your Github organization but you should **NEVER** commit directly in this repository.

### Initialization with the code

#### Student A

The first student, **student A** in your group will have to create a folder in his project named "alma-server". Inside this project, create a folder "src/main/java". The folder "alma-server" will be the root of your project and the folder "alma-server/src/main/java" will be your Java source folder. In this Java source folder, create a folder "fr/univnantes/alma/server" and inside, create the following Java class in a file named "Application.java":

```java
package fr.univnantes.alma.server;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

The **student A** will now commit this change in a branch named CODE with a [MEANINGFUL commit message](http://lmgtfy.com/?q=good+git+commit+message) and push it on his/her own copy of the Git repository in his/her Github account.

#### Student B

In the same time, the **student B** will improve the empty "README.md" file located at the root of the Git repository with the following content:

```md
### ALMA server

This repository will contain the source code of the ALMA server based on Spring Boot.
```

The **student B** will then commit in a branch named README his/her work and push it on his/her own Github repository on his/her own Github account.

#### Student C

The **student C** will start working on his/her clone of his/her repository in order to create the Git Ignore file. For that he/she will create a file named ".gitignore" at the root of the Git repository.

```
## This is the kind of files that we want to ignore
bin
target
*.class
*.jar
```

The **student C** will then commit it in a branch named GITIGNORE and push this branch to his/her Github repository.

#### All students

At this point, each of the student should have at least one commit on his/her Git repository and **NOTHING** should have changed on the Git repository of the organization. Now each student will create a pull request in order to contribute his/her state of his/her Git repository into the Git repository of the organization.

**CREATE ALL THE PULL REQUESTS IN THE GIT REPOSITORY OF THE ORGANIZATION FOR THE MASTER BRANCH OF THE ORGANIZATION**

As a result, the Git repository of the organization should have 3 pull requests awaiting to be integrated. Any student of your team not involved in the creation of a commit can review a pull request during this step (B or C for the pull request of A, etc).

Now you will merge the pull request of the **student C** first, then the **student B** and finally the **student A** using REBASE in order to have a linear history if the commit is valid. The history of the main repository should **ALWAYS** stay linear.

In order to do those kind of operations in all the parts of this project, you will NEED to accept the pull request with a rebase strategy in Github and to retrieve and rebase the changes from the main repository in your own repositories. Remember to **NEVER EVER EVER** rebase a commit that has been contributed to a remote repository! Those instructions will not be repeated after this steps even if you have to reproduce them (that's part of the test).

This first step should conclude with a linear history on the Git repository of the organization with four commits in the following (reversed) order:
- the contribution of the Java class
- the contribution to the file README.md
- the creation of the gitignore
- my initial commit

Retrieve the changes from the main central repository and update your own repository in order to have a master branch in your Git repository matching the state of the master branch of the Git repository of your organization. Each student should have created one commit with one branch, pushed it to his/her repository and submit one pull request with one commit to the main repository which now contains four commits. Do not remove anything, your temporary branches should be visible in your own Git repository (that why they have a specific name in this subject). Your grade will depend on what I can find in your Git repositories that includes your temporary branches!

### Setting up the maven based build

#### Student A

The **student A** will now configure the maven based build. For that, create a local branch named "MAVEN" from the new state of the master branch. In this branch, create a file named "pom.xml" in the folder "alma-server" with the following content:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>fr.univnantes</groupId>
    <artifactId>alma-server</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.4.2.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <properties>
        <java.version>1.8</java.version>
    </properties>


    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

Test your build with the command "mvn clean verify -e" in the "alma-server" folder then commit the creation of this new file in your "MAVEN" branch and push it to your Git repository. Create a pull request from your Git repository to the main repository.

#### Student C

Review the pull request for the creation of the pom.xml and add a comment indicating that the version of the pom.xml should change from "<version>0.1.0</version>" to "<version>1.0.0</version>".

#### Student A

Create another commit in your "MAVEN" branch in which you will change the version in the pom.xml, submit a new pull request to the main repository with this change.

#### Student C

The **student C** should now accept the new version of the pull request on the main Git repository.

### Adding support for Travis-CI

#### Student B

The **student B** will now add the first version of the support of the continuous integration. For that he/she will create a file named ".travis.yml" at the root of his/her Git repository in a branch named "TRAVIS". Set the following content in the file ".travis.yml":

```yaml
language: java
jdk: oraclejdk8

script:
  - cd alma-server/
  - mvn clean verify -e
```

The **student B** should then activate Travis support for the Git repository of the organization by going on the travis-ci.org website. After that, the **student B** will contribute its commit as a pull request on the main Git repository.

#### Student A

The **student A** will comment on the pull request to indicate that the ".travis.yml" file should be modified to have the following content:

```yaml
language: java
jdk: oraclejdk8

script:
  - mvn clean verify -f alma-server/pom.xml -e
```

#### Student B

The **student B** should create a new commit to modify the ".travis.yml" file and submit a new pull request with the new version of the file.

#### Student A

The **student A** should now accept the new version of the pull request on the main Git repository. The travis build should now be triggered and it should report its result.

### Add support for the creation of a Docker container

#### Student C

The **student C** will now be in charge of the creation of a Docker container using the result of the build. For that he/she will have to create a folder named "alma-server/src/main/docker". Inside he/she will have to create a file named "Dockerfile" with the following content:

```dockerfile
FROM frolvlad/alpine-oraclejdk8:slim
VOLUME /tmp
ADD alma-server-0.1.0-SNAPSHOT.jar app.jar
RUN sh -c 'touch /app.jar'
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Dspring.profiles.active=container","-jar","/app.jar"]
```

The **student C** will create a commit with this file in a branch named "DOCKER" in his/her Git repository and push it to his/her Git repository on Github, then he/she will create a pull request to the main Git repository of the organization.

#### Student B

The **student B** will then indicate with a comment that the **student C** has an error in his/het Docker file because the version of the project has been changed from 0.1.0 to 1.0.0.

#### Student C

The **student C** will have to change the reference to "alma-server-0.1.0-SNAPSHOT.jar" to "alma-server-1.0.0-SNAPSHOT.jar" in his/her Docker file. He/she will then have to create a new commit and a new pull request to the main repository.

#### Student B

The **student B** will have to accept this new pull request in the main Git repository.

### Add a controller in the server

#### Student B

The **student B** will now add a new controller in the web application. For that, he/she will create a new file named "HelloController.java" in the folder "alma-server/src/main/java/fr/univnantes/alma/server/controllers" with the following content:

```java
package fr.univnantes.alma.server.controllers;

import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Greetings from Spring Boot!";
    }

}
```

You can test your code with "mvn clean verify -e" in the folder containing the pom.xml and then "java -jar alma-server-1.0.0-SNAPSHOT.jar" in the folder "target" containing the artifacts created from the build. You can go to http://localhost:8080 to see the result of your server. The **student B** will now create a commit for this new file in a branch named "FIRST_CONTROLLER" and push it in his/her repository, using a pull request he/she will submit it to the main repository.

#### Student C

The **student C**  will integrate this pull request in the main repository if Travis mark the commit as having produced a successful build.

### Build the Docker container during the continuous integration

Create an account on [DockerHub](https://hub.docker.com/explore/) for your organization (do not use your personnal DockerHub account). Try to use the same name as your Github organization please. Then in the travis settings of the build of the main Git repository, enter the following variables:

* DOCKER_EMAIL
* DOCKER_USER
* DOCKER_PASSWORD

Do not show the value of those variables in the log during the build.

#### Student A

The **student A** should now plug the creation of the Docker container during the build. For that the **student A** will have to modify the pom.xml in order to add a new property juste after "java.version". This property will contain the name of your Docker Hub organization account:

```xml
<docker.image.prefix>ORGANIZATION_NAME</docker.image.prefix>
```

Then modify the "build" section of the pom.xml in order to have the following content instead:

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>com.spotify</groupId>
                <artifactId>docker-maven-plugin</artifactId>
                <version>0.4.11</version>
                <executions>
                    <execution>
                        <id>build-image</id>
                        <phase>package</phase>
                        <goals>
                            <goal>build</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>tag-image</id>
                        <phase>package</phase>
                        <goals>
                            <goal>tag</goal>
                        </goals>
                        <configuration>
                            <image>ORGANIZATION_NAME/alma-server:${project.version}</image>
                            <newName>hub.docker.com/ORGANIZATION_NAME/alma-server:${project.version}</newName>
                        </configuration>
                    </execution>
                </executions>
                <configuration>
                    <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
                    <dockerDirectory>${project.basedir}/src/main/docker</dockerDirectory>
                    <imageTags>
                        <imageTag>${project.version}</imageTag>
                        <imageTag>latest</imageTag>
                    </imageTags>
                    <resources>
                        <resource>
                            <targetPath>/</targetPath>
                            <directory>${project.build.directory}</directory>
                            <include>${project.build.finalName}.jar</include>
                        </resource>
                    </resources>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

**DO NOT FORGET TO REPLACE THE REFERENCES TO "ORGANIZATION_NAME"**

Modify also the ".travis.yml" to add support for Docker during the build

```yaml
sudo: required
services:
  - docker

language: java
jdk: oraclejdk8

branches:
  only:
    - master

before_install:
  - docker version
  - docker info

script:
  - mvn clean verify -f alma-server/pom.xml -e
```

Modify also the pom.xml in order to change the version number from 1.0.0 to 1.0.0-SNAPSHOT.

The **student A** should then create a commit in a new branch named "DOCKER_BUILD", push it to his/her Git repository and submit a pull requets to the main Git repository.

#### Student C

The **student C** should review and accept it if the Travis build is successful.

### Continuous release of the project

#### Student C

The **student C** will now be in charge of the release of the project. For that he/she will publish the Docker container built by Travis for each successful build. Modify the content of the file ".travis.yml" to the following content in order to add support for the publication of the Docker build:

```yaml
sudo: required
services:
  - docker

language: java
jdk: oraclejdk8

branches:
  only:
    - master

before_install:
  - docker version
  - docker info

script:
  - mvn clean verify -f alma-server/pom.xml -e

after_success:
  - docker login -e $DOCKER_EMAIL -u $DOCKER_USER -p $DOCKER_PASSWORD
  - docker images
  - docker push ORGANIZATION_NAME/alma-server:latest
```

**DO NOT FORGET TO REPLACE THE REFERENCES TO "ORGANIZATION_NAME"**

Create a commit on your Git repository in a new branch named "DOCKER_RELEASE", push it to your Git repository and submit a pull request on the main repository.

#### Student A

Accept the pull request if the build is successful of course. You project should now be available in DockerHub. Anyone with Docker should be able to run "docker run -p 8080:8080 ORGANIZATION_NAME/alma-server" and have your server up and running on http://localhost:8080

### Contribute a unit test in the project

#### Student B

The **student B** will contribute an unit test in the project. For that, he/she will create a file named "HelloControllerTest.java" in the folder "alma-server/src/test/java/fr/univnantes/alma/server/tests" with the following content:

```java
package fr.univnantes.alma.server.tests;

import static org.hamcrest.Matchers.equalTo;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class HelloControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void getHello() throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("Greetings from Spring Boot!")));
    }
}
```

Add the following dependency too in the pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Create a commit in a new branch named "TEST" and push it to your Git repository, then create a pull request on the main repository.

#### Student C

Accept the pull request if the Travis build is successful.

### Publish a Github release for each tagged commit

#### Student B

In a branch named "GITHUB_RELEASE", make sure that your Travis build publishes on Github a new release each time that a commit is tagged. Have a look at the Travis documentation for that: https://docs.travis-ci.com/user/deployment/releases/

##### Student A

Accept the pull request if you are confident with the change and of course if the build is successful. A release should be available in the release page of your project with the Jar created by the build.

### Add front end resources

#### Student C

The **student C** will create a file named index.html in the folder "alma-server/src/main/resources/static/" with the following content:

```html
<!DOCTYPE html>
<html>
<head>
<title>Static Resource</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>
	<div class="jumbotron">
		<h1>Home</h1>
		<p>Some static content</p>
	</div>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
    <!-- <script src="main.min.js"></script> -->
</body>
</html>
```

The JavaScript file "main.min.js" does not exist for the moment and it will be created by our continuous integration build. The **student C** will commit his/her work in a branch named STATIC and push it to his/her Git repository, after that he/she will submit a pull request to the main Git repository. If you launch the server, the URL http://localhost:8080/ will display the welcome message and the URL http://localhost:8080/index.html will show this static resource. Note that a proper web server would redirect the request to "/" to "/index.html" using a simple [resource](https://github.com/svalyn/svalyn/blob/master/svalyn-server/src/main/java/com/svalyn/server/controllers/IndexController.java).

#### Student B

The **student B** will accept the pull request if it works.


### Configure the build of your front end resources

#### Student A

The **student A** will create a file named "main.js" in the folder "static" next to the index.html file. The file main.js will have the following content:

```javascript
/*******************************************************************************
 * Copyright (c) 2017 <INSERT YOUR ORGANISATION NAME HERE>.
 * All rights reserved. This program and the accompanying materials
 * are made available under the terms of the MIT License which
 * accompanies this distribution, and is available at
 * https://opensource.org/licenses/MIT
 *******************************************************************************/
(function () {
    'use strict';

    var greatFunction = require('./folder/greatFunction');
    greatFunction();
})();
```

The **student A** will now create a second Javascript file used from the first one, as such we will create a graph of dependencies between our JavaScript files. Create a file named "greatFunction.js" in the folder "alma-server/src/main/resources/static/folder" with the following content:

```javascript
/*******************************************************************************
 * Copyright (c) 2017 <INSERT YOUR ORGANISATION NAME HERE>.
 * All rights reserved. This program and the accompanying materials
 * are made available under the terms of the MIT License which
 * accompanies this distribution, and is available at
 * https://opensource.org/licenses/MIT
 *******************************************************************************/
(function () {
    'use strict';

    var greatFunction = function () {
        alert('This is great!');
    };
    
    module.exports = greatFunction;
})();
```

This style of import using "require" and "module.exports" is also known as [CommonJS](https://nodejs.org/docs/latest/api/modules.html) and this is the standard way of managing imports between files in Node.js.

CommonJS works well but it has one issues, web browsers do not understand it. While the specification of ECMAScript 6 has defined a new syntax to import and export content between files, it has not defined yet how to load those modules. As a result, we will need to compile those modules into a single JavaScript file first in order to use it in our web page. The result of this build will produce our file named main.min.js because it will also be minified in order to remove comments. For that, the **student A** will now create a file named "package.json" in the folder "resources" with the following content:

```json
{
  "name": "alma-master",
  "version": "0.1.0",
  "description": "Simple web application",
  "private": true,
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/ORGANISATION_NAME/alma-m2-2016.git"
  },
  "keywords": [
    "alma"
  ],
  "author": "Stéphane Bégaudeau",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/ORGANISATION_NAME/alma-m2-2016/issues"
  },
  "homepage": "https://github.com/ORGANISATION_NAME/alma-m2-2016#readme",
  "devDependencies": {
    "browserify": "^13.1.0",
    "gulp": "^3.9.1",
    "gulp-browserify": "^0.5.1",
    "gulp-clean": "^0.3.2",
    "gulp-concat": "^2.6.0",
    "gulp-jshint": "^2.0.1",
    "gulp-load-plugins": "^1.2.4",
    "gulp-rename": "^1.2.2",
    "gulp-size": "^2.1.0",
    "gulp-uglify": "^2.0.0",
    "gulp-util": "^3.0.7",
    "jshint": "^2.9.3",
    "jshint-checkstyle-file-reporter": "0.0.1",
    "jshint-stylish": "^2.2.1"
  }
}
```

You can see in this file that we have the definition of all the developement tools that will be used to build the front end content of this project. Now you will create a file specifying how your project will be built. While we are using Maven for the Java build, here we will use Gulp as specified in the package.json file above. Create a file named "gulpfile.js" next to the file "package.json" in the folder "resources" with the following content:

```javascript
/*******************************************************************************
 * Copyright (c) 2017 <INSERT YOUR ORGANISATION NAME HERE>.
 * All rights reserved. This program and the accompanying materials
 * are made available under the terms of the MIT License which
 * accompanies this distribution, and is available at
 * https://opensource.org/licenses/MIT
 *******************************************************************************/

'use strict';

let gulp = require('gulp'),
    browserify = require('gulp-browserify'),
    gulpUtil = require('gulp-util');

var $ = require('gulp-load-plugins')();

gulp.task('clean', () => {
    return gulp.src([
        'static/main.min.js',
        'static/main.browserify.js',
        'checkstyle.xml'
    ]).pipe($.clean());
});

gulp.task('scripts', ['clean'], () => {
    return gulp.src(
        [
            'static/**/*.js'
        ])
        .pipe($.jshint())
        .pipe($.jshint.reporter(require('jshint-stylish')))
        .pipe($.jshint.reporter(require('jshint-checkstyle-file-reporter')))
        .pipe($.size());
});

gulp.task('browserify', ['scripts'], () => {
    return gulp.src(['static/main.js'])
        .pipe(browserify({insertGlobals: true}))
        .pipe($.concat('main.browserify.js'))
        .pipe(gulp.dest('static/'));
});

gulp.task('minify', ['browserify'], () => {
    return gulp.src(['static/main.browserify.js'])
        .pipe($.uglify().on('error', gulpUtil.log))
        .pipe($.rename('main.min.js'))
        .pipe(gulp.dest('static'))
});
```

With this gulp task, you can now clean the build artifact, create the browserify-ed version of the JavaScript file and minify it with uglify in order to create the file main.min.js. Now you need to define the static analysis rules of your project. For that create in the same folder a file named ".jshintrc" with the following content:

```json
{
  "esversion": 6,
  "node": true,
  "browser": true,
  "bitwise": true,
  "camelcase": true,
  "curly": true,
  "eqeqeq": true,
  "immed": true,
  "indent": 2,
  "latedef": true,
  "newcap": true,
  "noarg": true,
  "quotmark": "single",
  "regexp": true,
  "undef": true,
  "unused": true,
  "strict": true,
  "trailing": true,
  "smarttabs": true
}
```

Finally the **student A** will create a commit on a branch named STATIC_RESOURCES_BUILD and push it on his/her Git repository then he/she will submit a pull request on the main Git repository.

#### Student C

The **student C** will perform the code review of this pull request and integrate it if it works.


### Launch the build of your front end resources

#### Student B

The **student C** has created the static resources of the front end, the **student A** has created a build for them, now it is time to launch this build using our continuous integration server. For that, the **student B** will modify the build in the file ".travis.yml" to set the following content:

```yml
sudo: required
services:
  - docker

language: java
jdk: oraclejdk8

branches:
  only:
    - master

before_install:
  - docker version
  - docker info
  - node --version
  - npm --version

script:
  - cd alma-server/src/main/resources
  - pwd
  - npm install -g gulp
  - npm install
  - gulp minify
  - cd ../../../../
  - mvn clean verify -f alma-server/pom.xml -e

after_success:
  - docker login -e $DOCKER_EMAIL -u $DOCKER_USER -p $DOCKER_PASSWORD
  - docker images
  - docker push ORGANIZATION_NAME/alma-server:latest
```

The **student B** will also uncomment the line in the HTML file in order to load the file main.js: 

```html
<!DOCTYPE html>
<html>
<head>
<title>Static Resource</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>
	<div class="jumbotron">
		<h1>Home</h1>
		<p>Some static content</p>
	</div>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
    <script src="main.min.js"></script>
</body>
</html>
```

The **student B** will now push his/her commit on his/her Git repository in a branch named FRONT_END_BUILD and submit a pull request to the main Git repository. As a result, the continuous integration server on Travis-CI will now:

* install gulp (node.js and npm are installed by default in Travis)
* build the JavaScript file main.js (with gulp minify which will use browserify to navigate all the dependencies of the JavaScript file recursively)
* build the Java file in order to create a jar (which will contain the static resources built)

You should now have a project creating a simple web server with Java resources creating responses along with static resources in HTML and JavaScript. This server is built with various tools using a continuous integration server and its build publishes a Docker container for each change on the Docker Registry.

#### Student A

If the build is successful and if the review is good, the **student A** will integrate it.


### Deployment on any kind of cloud platform (bonus points)

You will have additional points if anybody in your group realize on of the following task:

* You deploy it on a Kubernetes cluster on Google Container Engine using [this tutorial](http://kubernetes.io/docs/hellonode/) (but with your own Docker image)
* You deploy it anywhere (AWS, GCE, GKE, DigitalOcean, Heroku, Linode, Azure, etc) but automatically after a successful build.



### Send the project back to the teacher

Create a pull request from the Git repository of your organization to my Git repository that you have forked in the beginning. Specify in the comment of the pull request or by email the name of the student A, B and C.
