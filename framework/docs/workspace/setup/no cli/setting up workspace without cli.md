# Setting up Umun Workspace

### Without using the [Umun CLI](../../../../../cli/README.md)

---

You may create a new umun workspace by either following the commands [step by step](#sbys), or simply
using [Umun CLI](../../../../../cli/README.md).

> It is recommended to use the [Umun CLI](../../../../../cli/README.md). You may choose to follow the given instructions if you wish to understand how the CLI works under the hood.

## Prerequisites

Check if you have the following installed or not on your system.

* Install [Node.js](https://nodejs.org/) 14 or higher, which
  includes [Node Package Manager](https://www.npmjs.com/get-npm)

```bash
$node --version

v14.17.0
```

* Install [Java SDK v1.8](https://www.java.com/) or higher.

```
$java -version

java version "1.8.0_231"
Java(TM) SE Runtime Environment (build 1.8.0_231-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.231-b11, mixed mode)
```

* Install [Maven](../../../installing%20maven.md)

```
mvn --version

Apache Maven 3.6.2
```

* Install [Spring CLI](../../../installing%20spring%20cli.md) v2.7.0 or higher

```
$ spring version

Spring CLI v2.7.0
```

* Install MySQL [TODO]
* Install Git [TODO]

---

## Step by step <a name="sbys"></a>


### 1. Create a new folder with your [PROJECT NAME].

```bash
mkdir [PROJECT NAME]
```

### 2. Change directory to product folder.

```
cd [PROJECT NAME]
```

### 3. Create backend project - using SpringBoot.
---

You can create this new project either using

A. [Spring CLI](#springcli)

B.  [Spring Starter](#springstarter) website.

C. Or can create a new project using eclipse or any of the [Spring Tools](https://spring.io/tools).

#### <a name="springcli"> </a> A. Spring CLI

More on [Spring CLI](https://docs.spring.io/spring-boot/docs/current/reference/html/cli.html)

1. Init a new project

```bash
spring init server -n umun-starter-project -g com.umun -a starter -v 0.0.1 --description "Demo project for Umun Framework [https://www.umun.in]" --package-name com.umun.starter  -d web,data-jpa,security,data-rest
```

> Change `<version>2.7.0</version>` to `<version>1.5.6</version>` in the `pom.xml` file inside the `server` folder.

> Change java version to 1.8. [TODO: Need to figure out why spring cli is using version  17 in pom.xml]

2. Install the following maven dependencies

```
mvn install:install-file -Dfile=./server/pom.xml -DgroupId="mysql" \
   -DartifactId="mysql-connector-java" -Dversion="5.1.46" -Dpackaging="packaging" -Dscope="runtime"
```


#### <a name="springstarter"></a> B. Spring Started

1. Go to [start.spring.io](start.spring.io)
2. Generate a project with the following configuration

![Spring starter config](./spring%20starter.png)

> The project shall have `Spring Web`, `Spring Data JPA` and `Spring Security` as dependencies.

> Choose Java 8

> You may choose group id and other details to your choice. 


### 4. Add the database connection properties

Add the following to `application.properties` file in `server/src/main/resources` folder.


```text
#MySQL Config
spring.datasource.url= jdbc:mysql://localhost:3306/[DATABASE NAME]
spring.datasource.username=[USERNAME]
spring.datasource.password=[PASSWORD]
spring.jpa.hibernate.ddl-auto=update

spring.data.rest.detection-strategy=annotated

#spring security
#You may enable this  later if using Spring Security
security.basic.enabled=false

```

> Make sure you have a database with the name `[DATABASE NAME]` that has a user with name `[USERNAME]` and its password is `[PASSWORD]`.

> You can always change the password, database name and username in the future to your liking.

#### Create a new database

You need to create a database in MySQL, where the backend will store its data.

* Install [MySQL](todo), if not already installed.
* Login to mysql

```
mysql -u [username] -p
```
> Enter password after you press enter. 

* Create a new database

```
create database [DATABASE NAME]
```

### 6. Change Spring Version

Change the project's Spring version to `<version>1.5.6.RELEASE</version>`
```bash
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.6.RELEASE</version> <!-- IMPORTANT for umun framework -->
    <relativePath /> <!-- lookup parent from repository -->
</parent>
```

### 8. Add Umun Module

From the following modules, import the required once to, `pom.xml`.

```
<dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>core</artifactId>
      <version>LATEST</version>
    </dependency>
    <dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>iam</artifactId>
      <version>LATEST</version>
    </dependency>
    <dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>entity</artifactId>
      <version>LATEST</version>
    </dependency>
    <dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>localization</artifactId>
      <version>LATEST</version>
    </dependency>
    <dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>system</artifactId>
      <version>LATEST</version>
    </dependency>
    <dependency>
      <groupId>in.umun.framework</groupId>
      <artifactId>user-pref</artifactId>
      <version>LATEST</version>
    </dependency>


    <!-- this is required to use any of the umun modules -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.46</version>
      <scope>runtime</scope>
    </dependency>
```

> You need to install the corresponding front-end modules as well.

### 9. Change directory back to the root

```
cd ..
```

```
$ pwd

... ./[PROJECT NAME]/
```

### 10. Create a new [Nx](todo) Workspace

```
npx create-nx-workspace [Organization Name] --preset=angular --appName=[App Name] --nxCloud=false --style=scss
```



