### Copy entire folder
task mytest << {
    copy {
        from fileTree('folder/mytest')
        into "mytest"
    }
}

### Debug
#### List folder contents
```
new File("${stageDir}").eachFile{ println it}
```

#### Run spring boot project with java params
Put this in build.gradle file
```
bootRun {
    systemProperty("spring.config.location", "src/main/docker/application.properties,../override.properties")
}
```
Then, usual run
```
gradle bootrun
```
### Run debug
```
gradle bootrun --debug-jvm
```
