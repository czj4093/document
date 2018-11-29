# 什么是Maven

Maven试图*将模式应用于项目的构建基础架构，以便通过提供使用最佳实践的明确路径来提高理解力和生产力*。Maven本质上是一个项目管理和理解工具，因此提供了一种帮助管理的方法：

- 构建
- 文档
- 报告
- 依赖
- 供应链管理系统
- 发布
- 分配

# Maven如何使我的开发过程受益

Maven可以通过采用标准约定和实践来加速您的开发周期，同时帮助您获得更高的成功率，从而为您的构建过程带来好处

# 我如何设置Maven

Maven的默认值通常已足够，但如果您需要更改缓存位置或位于HTTP代理后面，则需要创建配置。有关更多信息，请参阅[配置Maven指南](http://maven.apache.org/guides/mini/guide-configuring-maven.html)

# 我如何制作我的第一个Maven项目

要创建最简单的Maven项目，请从命令行执行以下命令：

```shell
mvn -B archetype:generate \
    -DarchetypeGroupId=org.apache.maven.archetypes \
    -DgroupId=com.mycompany.app \
    -DartifactId=my-app
```

执行完此命令后，已为新项目创建了一个名为`my-app`的目录，该目录包含一个名为`pom.xml`的文件，该文件应如下所示：

```xml-dtd
<project xmlns = “http://maven.apache.org/POM/4.0.0” 
	xmlns：xsi = “http://www.w3.org/2001/XMLSchema-instance”
	xsi：schemaLocation = “http://maven.apache.org/POM/4.0.0
	http://maven.apache.org/xsd/maven-4.0.0.xsd“ >
	<modelVersion> 4.0.0 </ modelVersion>
	<groupId> com.mycompany.app </ groupId>
    <artifactId> my-app </ artifactId>
    <packaging> jar</ packaging>
    <version> 1.0-SNAPSHOT </ version>
    <name> Maven Quick Start Archetype </ name>
    <url> http://maven.apache.org </ url>
    <dependencies>
        <dependency>
            <groupId> junit </ groupId>
            <artifactId> junit </ artifactId>
            <version> 4.11 </ version>
            <scope> test </ scope>
        </dependency>
    </dependencies>
</project>
```

`pom.xml`包含此项目的项目对象模型（POM）。POM是Maven的基本工作单元。这一点很重要，因为Maven本质上是以项目为中心的，因为一切都围绕着项目的概念。简而言之，POM包含有关您项目的所有重要信息，并且基本上是一站式购物，用于查找与您的项目相关的任何内容。了解POM很重要，鼓励新用户参考[POM简介](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)。

这是一个非常简单的POM，但仍然显示每个POM包含的关键元素，所以让我们通过每个POM来熟悉POM要点：

- **project**这是所有Maven pom.xml文件中的顶级元素。
- **modelVersion**此元素指示此POM使用的对象模型的版本。模型本身的版本很少发生变化，但如果Maven开发人员认为有必要更改模型，则必须确保使用的稳定性。
- **groupId**此元素指示创建项目的组织或组的唯一标识符。groupId是项目的关键标识符之一，通常基于组织的完全限定域名。例如，`org.apache.maven.plugins`是所有Maven插件的指定groupId。
- **artifactId**此元素指示此项目生成的主工件的唯一基本名称。项目的主要工件通常是JAR文件。像源包这样的辅助工件也使用artifactId作为其最终名称的一部分。Maven生成的典型工件将具有<artifactId> - <version>。<extension>形式（例如，`myapp-1.0.jar`）。
- **packaging**此元素指示此工件要使用的包类型（例如JAR，WAR，EAR等）。这不仅意味着生成的工件是JAR，WAR还是EAR，还可以指示要在构建过程中使用的特定生命周期。（生命周期是我们将在指南中进一步讨论的主题。现在，请记住，项目的指示包装可以在定制构建生命周期中发挥作用。）`包装`元素的默认值是JAR所以你不必为大多数项目指定这个。
- **version**此元素指示项目生成的工件的版本。Maven在很大程度上帮助您进行版本管理，您经常会在一个版本中看到`SNAPSHOT`指示符，这表明项目处于开发状态。我们将在本指南中讨论[快照](http://maven.apache.org/guides/getting-started/index.html#What_is_a_SNAPSHOT_version)的使用以及它们如何进一步工作。
- **name**此元素指示用于项目的显示名称。这通常用于Maven生成的文档中。
- **url**此元素指示可以找到项目站点的位置。这通常用于Maven生成的文档中。
- **description**此元素提供项目的基本描述。这通常用于Maven生成的文档中。

# 如何编译我的应用程序源

切换到archetype创建pom.xml的目录：生成并执行以下命令来编译应用程序源：

```shell
mvn compile
```

# 如何编译测试源并运行单元测试

现在你已经成功编译了应用程序的源代码，现在你已经有了一些你想要编译和执行的单元测试（因为每个程序员总是编写并执行他们的单元测试* nudge nudge wink wink *）。

执行以下命令：

```shell
mvn test
```

如果您只想编译测试源（但不执行测试），则可以执行以下操作：

```shell
mvn test - compile
```

# 如何创建JAR并将其安装在本地存储库中

制作JAR文件非常简单，可以通过执行以下命令来完成：

```shell
mvn package
```

如果您查看项目的POM，您会注意到`包装`元素设置为`jar`。这就是Maven如何通过上面的命令生成JAR文件（稍后我们将详细讨论）。您现在可以查看`$ {basedir} / target`目录，您将看到生成的JAR文件。

现在，您需要在本地存储库中安装您生成的工件（JAR文件）（`$ {user.home} /.m2 / repository`是默认位置）。有关存储库的更多信息，请参阅我们的[存储库简介，](http://maven.apache.org/guides/introduction/introduction-to-repositories.html)但让我们继续安装我们的工件！为此，请执行以下命令：

```shell
mvn install
```

# 什么是SNAPSHOT版本

请注意，下面显示的`pom.xml`文件中的**version**标记的值具有后缀：`-SNAPSHOT`

```xml
<project xmlns =“http://maven.apache.org/POM/4.0.0”  ...  
	<groupId> ... </ groupId>  
	<artifactId> my-app </ artifactId>  ...  
	<version> 1.0-SNAPSHOT </ version>  
	<name> Maven Quick Start Archetype </ name>  ...
```

该`快照`值指的是沿着一个发展分支的“最新”的代码，并且不保证该代码是稳定的或不变。相反，“发布”版本中的代码（没有后缀`SNAPSHOT的`任何版本值）都是不变的。

换句话说，SNAPSHOT版本是最终'发布'版本之前的'开发'版本。SNAPSHOT比其版本“更老”。

在[发布](http://maven.apache.org/plugins/maven-release-plugin/)过程中，**xy-SNAPSHOT**的版本更改为**xy**。发布过程还将开发版本增加到**x。（y + 1）-SNAPSHOT**。例如，版本**1.0-SNAPSHOT**作为版本**1.0**发布，新版本版本版本为**1.1-SNAPSHOT**

# 我如何使用插件

配置Java编译器版本JDK 5.0

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.3</version>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

# 如何向JAR添加资源

`$ {basedir} / src / main / resources`目录中的任何目录或文件都打包在JAR中

# 如何过滤资源文件

有时，资源文件需要包含只能在构建时提供的值。要在Maven中完成此操作，请使用语法`$ {<property name>}`将包含值的属性引用到资源文件中。该属性可以是pom.xml中定义的值之一，用户settings.xml中定义的值，外部属性文件中定义的属性或系统属性。

要在复制时让Maven过滤资源，只需为`pom.xml中`的resource directory设置`filtering`为true ：

```xml-dtd
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
 
  <name>Maven Quick Start Archetype</name>
  <url>http://maven.apache.org</url>
 
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
 
  <build>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
      </resource>
    </resources>
  </build>
</project>
```

要引用pom.xml中定义的属性，属性名称使用定义值的XML元素的名称，允许“pom”作为项目（根）元素的别名。所以`$ {project.name}`指的是项目的名称，`$ {project.version}`指的是项目的版本，`$ {project.build.finalName}`指的是建立项目时创建的文件的最终名称包装等等。请注意，POM的某些元素具有默认值，因此不需要在`pom.xml中`明确定义此处可用的值。同样，可以使用以“settings”开头的属性名称引用用户`settings.xml`中的值（例如，`$ {settings.localRepository}`指的是用户本地存储库的路径

```properties
# application.properties
application.name=${project.name}
application.version=${project.version}
```

# 我如何使用外部依赖项

pom.xml 的`dependencies`部分列出了我们的项目构建所需的所有外部依赖项（在编译时是否需要该依赖项，测试时间，运行时间等）

对于每个外部依赖项，您需要至少定义4个内容：groupId，artifactId，version和scope。groupId，artifactId和version与构建该依赖项的项目的`pom.xml中`给出的相同。scope元素指示项目如何使用该依赖项，并且可以是诸如`compile`，`test`和`runtime之类的值`。有关可以为依赖项指定的所有内容的更多信息，请参阅“ [项目描述符参考”](http://maven.apache.org/ref/current/maven-model/maven.html)

有了依赖关系的这些信息，Maven将能够在构建项目时引用依赖关系。Maven在哪里引用依赖关系？Maven查找您的本地存储库（`$ {user.home} /.m2 / repository`是默认位置）以查找所有依赖项。在[上一节中](http://maven.apache.org/guides/getting-started/index.html#How_do_I_create_a_JAR_and_install_it_in_my_local_repository)，我们将项目（my-app-1.0-SNAPSHOT.jar）中的工件安装到本地存储库中

每当项目引用本地存储库中不可用的依赖项时，Maven就会将依赖项从远程存储库下载到本地存储库中。您可能已经注意到Maven在构建您的第一个项目时下载了很多东西（这些下载是用于构建项目的各种插件的依赖项）。默认情况下，可以在<http://repo.maven.apache.org/maven2/>找到（并浏览）Maven使用的远程存储库。您也可以使用自己的远程存储库（可能是公司的中央存储库）来代替默认远程存储库或使用默认远程存储库。有关存储库的更多信息，请参阅[存储库简介](http://maven.apache.org/guides/introduction/introduction-to-repositories.html)

# 如何在远程存储库中部署jar

要将jar部署到外部存储库，您必须在pom.xml中配置存储库URL，并在settings.xml中配置连接到存储库的身份验证信息。

以下是使用scp和用户名/密码身份验证的示例

```xml-dtd
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
 
  <name>Maven Quick Start Archetype</name>
  <url>http://maven.apache.org</url>
 
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.apache.codehaus.plexus</groupId>
      <artifactId>plexus-utils</artifactId>
      <version>1.0.4</version>
    </dependency>
  </dependencies>
 
  <build>
    <filters>
      <filter>src/main/filters/filters.properties</filter>
    </filters>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
      </resource>
    </resources>
  </build>
  <!--
   |
   |
   |
   -->
  <distributionManagement>
    <repository>
      <id>mycompany-repository</id>
      <name>MyCompany Repository</name>
      <url>scp://repository.mycompany.com/repository/maven2</url>
    </repository>
  </distributionManagement>
</project>
```

```xml-dtd
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">
  ...
  <servers>
    <server>
      <id>mycompany-repository</id>
      <username>jvanzyl</username>
      <!-- Default value is ~/.ssh/id_dsa -->
      <privateKey>/path/to/identity</privateKey> (default is ~/.ssh/id_dsa)
      <passphrase>my_key_passphrase</passphrase>
    </server>
  </servers>
  ...
</settings>
```

请注意，如果要连接到在sshd_confing中将参数“PasswordAuthentication”设置为“no”的openssh ssh服务器，则每次都需要输入密码进行用户名/密码验证（尽管您可以使用其他ssh登录）客户端输入用户名和密码）。在这种情况下，您可能希望切换到公钥身份验证。

如果在`settings.xml中`使用密码，则应该小心。有关更多信息，请参阅[密码加密](http://maven.apache.org/guides/mini/guide-encryption.html)