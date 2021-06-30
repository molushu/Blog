---

title: NSFileManager操作和管理文件
date: 2021-06-30 12:47:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630124905.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630125036.png">



```objective-c
- (void)_getSandBoxPath {
    NSArray *pathArray = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);
    NSString *cachePath = [pathArray firstObject];
    
    NSFileManager *fileManager = [NSFileManager defaultManager];
    
    //创建文件夹
    NSString *dataPath = [cachePath stringByAppendingPathComponent:@"GTData"];
    NSError *creatError;
    [fileManager createDirectoryAtPath:dataPath withIntermediateDirectories:YES attributes:nil error:&creatError];
    
    //创建文件
    NSString *listDataPath = [dataPath stringByAppendingPathComponent:@"list"];
    NSData *listData = [@"abc" dataUsingEncoding:NSUTF8StringEncoding];
    [fileManager createFileAtPath:listDataPath contents:listData attributes:nil];
    
    //查询文件
    BOOL fileExist = [fileManager fileExistsAtPath:listDataPath];
    
    //删除
//    if (fileExist) {
//        [fileManager removeItemAtPath:listDataPath error:nil];
//    }
    
    NSLog(@"");
    
    NSFileHandle *fileHandler = [NSFileHandle fileHandleForUpdatingAtPath:listDataPath];
    
    [fileHandler seekToEndOfFile];
    [fileHandler writeData:[@"def" dataUsingEncoding:NSUTF8StringEncoding]];
    
    [fileHandler synchronizeFile];
    [fileHandler closeFile];
}
```



