---

title: NSThread
date: 2021-07-01 23:32:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210701233421.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210701233650.png">



```objective-c
NSThread *downloadImageThread = [[NSThread alloc] initWithBlock:^{
        UIImage *image = [UIImage imageWithData:[NSData dataWithContentsOfURL:[NSURL URLWithString:item.picUrl]]];
        self.rightImageView.image = image;
    }];
    
    downloadImageThread.name = @"downloadImageThread";
    [downloadImageThread start];
```



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210701234103.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210701234125.png">
