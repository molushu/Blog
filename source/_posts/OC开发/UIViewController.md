---

title: UIViewController
date: 2021-06-9 17:06:44
categories: 
- OC开发
---

## 1、ViewController的生命周期

```objective-c
init
viewDidLoad
viewWillAppear
viewDidAppear

viewWillDisappear
viewDidDisappear
Dealloc
```





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

//通过重写UIViewController类中的一些方法，来观察UIViewController的生命周期
@implementation ViewController

- (instancetype)init {
    self = [super init];
    if (self) {
        
    }
    return self;
}

- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];
}

- (void)viewDidAppear:(BOOL)animated{
    [super viewDidAppear:animated];
}

- (void)viewWillDisappear:(BOOL)animated{
    [super viewWillDisappear:animated];
}

- (void)viewDidDisappear:(BOOL)animated{
    [super viewDidDisappear:animated];
}

- (void)viewDidLoad {
    [super viewDidLoad];
    
    TestView *view1 = [[TestView alloc] init];
    view1.backgroundColor = [UIColor greenColor];
    view1.frame = CGRectMake(150, 150, 100, 100);
    [self.view addSubview:view1];
}

@end
```

