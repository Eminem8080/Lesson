### 1.Gradle与Gradlew Plugin 对应版本

| Plugin version | Required Gradle version |
| -------------- | ----------------------- |
| 1.0.0 - 1.1.3  | 2.2.1 - 2.3             |
| 1.2.0 - 1.3.1  | 2.2.1 - 2.9             |
| 1.5.0          | 2.2.1 - 2.13            |
| 2.0.0 - 2.1.2  | 2.10 - 2.13             |
| 2.1.3 - 2.2.3  | 2.14.1+                 |
| 2.3.0+         | 3.3+                    |
| 3.0.0+         | 4.1+                    |
| 3.1.0+         | 4.4+                    |
| 3.2.0 - 3.2.1  | 4.6+                    |
| 3.3.0 - 3.3.2  | 4.10.1+                 |
| 3.4.0 - 3.4.1  | 5.1.1+                  |
| 3.5.0          | 5.4.1+                  |

### 2.Gradle连接不上google拉去文件受阻碍

修改gradle的maven地址为国内镜像：修改**project**中的**build**文件；其中**buildscript**中的**repositories**在此处添加国内镜像:**maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }** 以及**allprojects**中的**repositories**同样也要添加。

