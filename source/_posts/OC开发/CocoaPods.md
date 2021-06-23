---

title: CocoaPods
date: 2021-06-23 23:17:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623231935.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623232053.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623232232.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623232405.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/D1FC6528-83C0-4BA4-B538-2D5309F381EC.png">



终端输入pod init，既可生成Podfile文件

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623232923.png">

Podfile文件中写入pod 'AFNetworking'

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623233102.png">

终端输入pod install，既可生成Podfile.lock文件、Pods文件夹、.xcworkspace文件

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210623233234.png">



```objective-c
#import "GTListLoader.h"
#import <AFNetworking.h>

@implementation GTListLoader

- (void)loadListData {
    [[AFHTTPSessionManager manager] GET:@"http://v.juhe.cn/toutiao/index?type=top&key=97ad001bfcc2082e2eeaf798bad3d54e" parameters:nil headers:nil progress:^(NSProgress * _Nonnull downloadProgress) {
            
        } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
            NSLog(@"");
        } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
            NSLog(@"");
        }];
    
    
//    NSString *urlString = @"https://www.baidu.com";
//    NSURL *listURL = [NSURL URLWithString:urlString];
////    NSURLRequest *listRequset = [NSURLRequest requestWithURL:listURL];
//    NSURLSession *session = [NSURLSession sharedSession];
////    NSURLSessionDataTask *dataTask = [session dataTaskWithRequest:listRequset];
//    NSURLSessionDataTask *dataTask = [session dataTaskWithURL:listURL completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
//        NSLog(@"");
//    }];
//
//    [dataTask resume];
//
//    NSLog(@"");
    
}

@end
```

