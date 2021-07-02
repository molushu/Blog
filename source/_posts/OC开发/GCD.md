---

title: GCD
date: 2021-07-02 12:24:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210702122718.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210702123001.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210702123202.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210702123417.png">



```objective-c
//非主线程
dispatch_queue_global_t downloadQueue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
//主线程
dispatch_queue_main_t mainQueue = dispatch_get_main_queue();

//非主线程，异步执行高耗时操作
dispatch_async(downloadQueue, ^{
  UIImage *image = [UIImage imageWithData:[NSData dataWithContentsOfURL:[NSURL URLWithString:item.picUrl]]];
  //主线程，异步执行UI操作
  dispatch_async(mainQueue, ^{
    self.rightImageView.image = image;
  });
});
```


