---
title: UIView
date: 2021-06-9 12:50:44
categories: 
- OC开发
---

## 1、添加子view

```objective-c
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    //如果有重叠区域，后面添加的子view会覆盖之前添加的子view重叠区域
    UIView *view1 = [[UIView alloc] init];
    view1.backgroundColor = [UIColor redColor];
    view1.frame = CGRectMake(100, 100, 100, 100);
    [self.view addSubview:view1];
    
    UIView *view2 = [[UIView alloc] init];
    view2.backgroundColor = [UIColor greenColor];
    view2.frame = CGRectMake(150, 150, 100, 100);
    [self.view addSubview:view2];
    
}

@end
```

## 效果：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210609123220.png">



## 2、UIView生命周期函数执行顺序

```objective-c
#import "ViewController.h"

@interface TestView : UIView

@end

//定义UIView的一个子类TestView,通过重写UIView类中的一些方法，来观察UIView的生命周期
@implementation TestView

- (instancetype)init {
    self = [super init];
    if (self) {
        
    }
    return self;
}

- (void)willMoveToSuperview:(nullable UIView *)newSuperview {
    [super willMoveToSuperview:newSuperview];
}

- (void)didMoveToSuperview {
    [super didMoveToSuperview];
}

- (void)willMoveToWindow:(nullable UIWindow *)newWindow {
    [super willMoveToWindow:newWindow];
}

- (void)didMoveToWindow {
    [super didMoveToWindow];
}

@end

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    TestView *view1 = [[TestView alloc] init];
    view1.backgroundColor = [UIColor greenColor];
    view1.frame = CGRectMake(150, 150, 100, 100);
    [self.view addSubview:view1];
}

@end
```

## 效果：

打上断点进行调试，依次执行如下代码：

```objective-c
TestView *view1 = [[TestView alloc] init];
- (instancetype)init；
[self.view addSubview:view1];
- (void)willMoveToSuperview:(nullable UIView *)newSuperview；
- (void)didMoveToSuperview；
- (void)willMoveToWindow:(nullable UIWindow *)newWindow；
- (void)didMoveToWindow；
```

