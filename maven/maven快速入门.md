# 新建项目

某处创建一个目录并在该目录中启动一个shell。在命令行上，执行以下Maven命令

```shell
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

创建了一个与artifactId具有相同名称的目录

## POM

`pom.xml`文件是在Maven中项目的配置核心。它是一个单一的配置文件，包含以您希望的方式构建项目所需的大部分信息。POM是巨大的，其复杂性可能令人生畏，但没有必要了解所有错综复杂的有效使用它。这个项目的POM是

```xml-dtd
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.mycompany.app</groupId>
  <artifactId>my-app</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>my-app</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```

## 打包

```shell
mvn package
```

执行阶段：

1. 验证
2. 产生来源
3. 流程源
4. 生成资源
5. 流程资源
6. 编译

# 运行Maven工具

## Maven阶段

虽然不是一个全面的列表，但这些是最常见的*默认*生命周期阶段。

- **validate**：验证项目是否正确并且所有必要信息都可用
- **compile**：编译项目的源代码
- **test**：使用合适的单元测试框架测试编译的源代码。这些测试不应要求打包或部署代码
- **package**：获取已编译的代码并将其打包为可分发的格式，例如JAR。
- **integration-test**：如有必要，将程序包处理并部署到可以运行集成测试的环境中
- **verify**：运行任何检查以验证包是否有效并符合质量标准
- **install**：将软件包安装到本地存储库中，以便在本地用作其他项目的依赖项
- **deploy**：在集成或发布环境中完成，将最终包复制到远程存储库以与其他开发人员和项目共享。

除了上面的*默认*列表之外，还有另外两个Maven生命周期。他们是

- **clean**：清除先前构建创建的工件

- **site**：为该项目生成站点文档

阶段实际上映射到基本目标。每个阶段执行的具体目标取决于项目的包装类型。例如，如果项目类型是JAR，则*包*执行*jar：jar，*如果项目类型是*war，*则执行*war：war* - 你猜对了 - 一个WAR。

值得注意的一点是，阶段和目标可以按顺序执行。

```shell
mvn clean dependency:copy - dependencies package
```

此命令将清理项目，复制依赖项并打包项目（当然，执行所有阶段直到*包*）

## 生成网站

```shell
mvn site
```

此阶段根据项目的pom信息生成站点。您可以查看`target / site`下生成的文档