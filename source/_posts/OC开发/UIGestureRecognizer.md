---

title: UIGestureRecognizer
date: 2021-06-16 10:18:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616104443.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616104742.png">



```objective-c
#import "GTRecommendViewController.h"

@interface GTRecommendViewController () <UIScrollViewDelegate, UIGestureRecognizerDelegate>

@end

@implementation GTRecommendViewController

- (instancetype) init {
    self = [super init];
    if (self) {
        self.tabBarItem.title = @"推荐";
        self.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/like@2x.png"];
        self.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/like_selected@2x.png"];
    }
    
    return self;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    UIScrollView *scrollView = [[UIScrollView alloc] initWithFrame:self.view.bounds];
    scrollView.backgroundColor = [UIColor lightGrayColor];
    scrollView.contentSize = CGSizeMake(self.view.bounds.size.width * 5, self.view.bounds.size.height);
    scrollView.delegate = self;
    NSArray *colorArray = @[[UIColor redColor], [UIColor blueColor], [UIColor yellowColor], [UIColor lightGrayColor], [UIColor grayColor]];
    
    for (int i = 0; i < 5; i++) {
        UIView *view = [[UIView alloc] initWithFrame:CGRectMake(scrollView.bounds.size.width * i, 0, scrollView.bounds.size.width, scrollView.bounds.size.height)];
        view.backgroundColor = [colorArray objectAtIndex:i];
        [scrollView addSubview:view];
        
        UIView *view1 = [[UIView alloc] initWithFrame:CGRectMake(100, 200, 100, 100)];
        view1.backgroundColor = [UIColor yellowColor];
        UITapGestureRecognizer *tapGesture = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(viewClick)];
        tapGesture.delegate = self;
        [view addGestureRecognizer:tapGesture];
        [view addSubview:view1];
    }
    
    scrollView.pagingEnabled = YES;
    [self.view addSubview:scrollView];
}

- (void)viewClick {
    NSLog(@"viewClick");
}

- (BOOL)gestureRecognizerShouldBegin:(UIGestureRecognizer *)gestureRecognizer {
    return YES;
}

- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
//    NSLog(@"scrollViewDidScroll - %@", @(scrollView.contentOffset.x));
}

- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView {
    NSLog(@"BeginDragging");
}

- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate {
    NSLog(@"EndDragging");
}

- (void)scrollViewWillBeginDecelerating:(UIScrollView *)scrollView {
    
}

- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView {
    
}

@end
```



## 效果

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616105641.png">
