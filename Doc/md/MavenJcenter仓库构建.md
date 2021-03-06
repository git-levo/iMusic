apply plugin: 'com.android.library'
apply plugin: 'maven'
apply plugin: 'com.novoda.bintray-release'

android {
    compileSdkVersion 26

    defaultConfig {
        minSdkVersion 16
        targetSdkVersion 26
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    //编译发布至Bintray时报错处理
    lintOptions {
        abortOnError false
    }
}

//推送到Bintray配置
publish {
    //你的账户bintray下某个组织id
    userOrg = rootProject.ext.userOrg
    //Maven仓库下库的包名,一本与包名相同
    groupId = rootProject.ext.groupId
    //开源协议
    licences = rootProject.ext.licences
    //项目名称
    artifactId = 'msuic-player-lib'
    //版本号
    publishVersion = '1.0.0'
    //项目介绍，可以不写
    desc = 'Android MusicPlayer Library'
    //项目主页，可以不写
    website = 'https://github.com/Yuye584312311/IMusic'
}

//生成到本地Maven仓库的task
uploadArchives{
    repositories.mavenDeployer{
        // 配置本地仓库路径，这里是项目的根目录下的maven目录中
        repository(url: uri('../maven'))
        // 唯一标识 一般为模块包名 也可其他
        pom.groupId = "com.android.imusic.lib"
        // 项目名称（一般为模块名称 也可其他
        pom.artifactId = "music-player-lib"
        // 发布的版本号
        pom.version = "1.0.0"
    }
}

dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
    implementation 'com.android.support:appcompat-v7:26.1.0'
    implementation 'com.android.support:recyclerview-v7:26.1.0'
    implementation 'com.android.support:design:26.1.0'
    implementation 'com.android.support.constraint:constraint-layout:1.0.2'
    implementation 'com.github.bumptech.glide:glide:3.7.0'
    implementation 'jp.wasabeef:glide-transformations:2.0.1'
}