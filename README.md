gradle-bintray-upload
==

[Android Studio上传Library库到JCenter，并同步到Maven Central](http://blog.csdn.net/venshine/article/details/51742926)

bintray.gradle：发布到JCenter的脚本  

build.gradle：配置项目根目录下的发布插件  

gradle.properties：在bintray.gradle中使用到的属性配置文件  

local.properties：账号信息等私人数据  

### 1.修改项目根目录下的build.gradle文件  
参考本项目的[build.gradle](https://github.com/venshine/gradle-bintray-upload/blob/master/build.gradle)，修改项目里的build.gradle（注意是项目不是库），增加以下两个dependencies：
``` groovy
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.6'
classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
```

### 2.修改Library下的build.gradle文件
在build.gradle文件底部添加以下代码：  
``` groovy
apply from: 'https://raw.githubusercontent.com/venshine/gradle-bintray-upload/master/bintray.gradle'
```
如果提示：Gradle sync failed: Software caused connection abort: recv failed。替换上面的内容为以下代码：
``` groovy
apply from: 'http://git.oschina.net/venshine/gradle-bintray-upload/raw/master/bintray.gradle'
```

### 3.配置gradle.properties文件
参考本项目下的[gradle.properties](https://github.com/venshine/gradle-bintray-upload/blob/master/gradle.properties)文件，对以下内容替换为自己的信息：
```
PROJ_GROUP=com.wx.android.common
PROJ_VERSION=1.0.3
PROJ_NAME=AndroidCommon
PROJ_WEBSITEURL=https://github.com/venshine/AndroidCommon
PROJ_ISSUETRACKERURL=https://github.com/venshine/AndroidCommon/issues
PROJ_VCSURL=https://github.com/venshine/AndroidCommon.git
PROJ_DESCRIPTION=Android Common Library
PROJ_ARTIFACTID=AndroidCommon

LICENSE_NAME='The Apache Software License, Version 2.0'
LICENSE_URL='http://www.apache.org/licenses/LICENSE-2.0.txt'

DEVELOPER_ID=venshine
DEVELOPER_NAME=venshine
DEVELOPER_EMAIL=venshine.cn@gmail.com
```

### 4.配置bintray帐号信息
参考本项目下的[local.properties](https://github.com/venshine/gradle-bintray-upload/blob/master/local.properties)文件，对以下内容替换为自己的信息：
```
bintray.user=your_bintray_user_name
bintray.apikey=your_bintray_api_key
bintray.gpg.password=your_pgp_password
bintray.oss.user=your_maven_central_user_name
bintray.oss.password=your_maven_central_password
```

### 5.执行命令
项目根目录下执行以下命令将库发布到[bintray](https://bintray.com/)。
```
gradlew install
gradlew bintrayUpload
```

### 6.Add to Jcenter
登录[Bintray](https://bintray.com/)网站，去自己的仓库首页，找到该库，点击Add to JCenter按钮，然后发送消息，等待审核结果，一般几个小时的时间就会审核通过。以后再更新项目上传到Bintray就不需要再次审核了。
