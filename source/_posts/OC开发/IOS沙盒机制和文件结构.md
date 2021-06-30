---

title: IOS沙盒机制和文件结构
date: 2021-06-30 10:56:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630105944.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630110225.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630110517.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/75EA9EA5-1F36-4460-8766-7C5C27192983.png">



```objective-c
- (void)_getSandBoxPath {
    NSArray *pathArray = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    
    NSLog(@"");
}
```



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210630111223.png">
