---


title: UINavigationController
date: 2021-06-9 23:24:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/4174D3B9-7C3E-4C9E-AF2B-B2F5387125DB.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210609233230.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210609233402.png">

```objective-c
- (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session options:(UISceneConnectionOptions *)connectionOptions {
    // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
    // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
    // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
    
    self.window = [[UIWindow alloc] initWithWindowScene:(UIWindowScene *)scene];
    
    UITabBarController *tabbarController = [[UITabBarController alloc] init];
    
    ViewController *viewController = [[ViewController alloc] init];
    
    UINavigationController *myNavigationController = [[UINavigationController alloc] initWithRootViewController:viewController];
    myNavigationController.tabBarItem.title = @"新闻";
    myNavigationController.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/page@2x.png"];
    myNavigationController.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/page_selected@2x.png"];
    
    UIViewController *controller2 = [[UIViewController alloc] init];
    controller2.view.backgroundColor = [UIColor yellowColor];
    controller2.tabBarItem.title = @"视频";
    controller2.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/video@2x.png"];
    controller2.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/video_selected@2x.png"];
    
    UIViewController *controller3 = [[UIViewController alloc] init];
    controller3.view.backgroundColor = [UIColor greenColor];
    controller3.tabBarItem.title = @"推荐";
    controller3.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/like@2x.png"];
    controller3.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/like_selected@2x.png"];
    
    UIViewController *controller4 = [[UIViewController alloc] init];
    controller4.view.backgroundColor = [UIColor lightGrayColor];
    controller4.tabBarItem.title = @"我的";
    controller4.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/home@2x.png"];
    controller4.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/home_selected@2x.png"];
    
    [tabbarController setViewControllers:@[myNavigationController, controller2, controller3, controller4]];
    
    self.window.rootViewController = tabbarController;
    [self.window makeKeyAndVisible];
}
```



ViewController.m文件

```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    TestView *view1 = [[TestView alloc] init];
    view1.backgroundColor = [UIColor greenColor];
    view1.frame = CGRectMake(150, 150, 100, 100);
    [self.view addSubview:view1];
    
    UITapGestureRecognizer *tapGesture = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(pushController)];
    [view1 addGestureRecognizer:tapGesture];
}

- (void)pushController {
    UIViewController *viewController = [[UIViewController alloc] init];
    viewController.view.backgroundColor = [UIColor whiteColor];
    viewController.navigationItem.title = @"内容";
    
    viewController.navigationItem.rightBarButtonItem = [[UIBarButtonItem alloc] initWithTitle:@"右侧标题" style:UIBarButtonItemStylePlain target:self action:nil];
    
    [self.navigationController pushViewController:viewController animated:YES];
}
```



## 效果：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210610001431.png">

点击绿色区域后展示页面：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210610001506.png">

