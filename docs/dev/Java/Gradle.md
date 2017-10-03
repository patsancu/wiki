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
