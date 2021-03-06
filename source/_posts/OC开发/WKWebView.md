---

title: WKWebView
date: 2021-06-16 17:04:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616180128.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616180609.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616180922.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/2480E7FF-6C91-4689-A714-204B4451C4C8.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/66188906-D513-4E45-B49F-D1EB0362DAD5.png">



```objective-c
#import "GTDetailViewController.h"
#import <WebKit/WebKit.h>

@interface GTDetailViewController () <WKNavigationDelegate>

@property(nonatomic, strong, readwrite) WKWebView *webView;
@property(nonatomic, strong, readwrite) UIProgressView *progressView;

@end

@implementation GTDetailViewController

- (void)dealloc {
    [self.webView removeObserver:self forKeyPath:@"estimatedProgress"];
}

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.webView = [[WKWebView alloc] initWithFrame:CGRectMake(0, 80, self.view.frame.size.width, self.view.frame.size.height - 88)];
    self.webView.navigationDelegate = self;
    [self.view addSubview:_webView];
    
    self.progressView = [[UIProgressView alloc] initWithFrame:CGRectMake(0, 88, self.view.frame.size.width, 20)];
    [self.view addSubview:_progressView];
    
    [self.webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"https://www.baidu.com"]]];

    [self.webView addObserver:self forKeyPath:@"estimatedProgress" options:NSKeyValueObservingOptionNew context:nil];
}

- (void)webView:(WKWebView *)webView decidePolicyForNavigationAction:(WKNavigationAction *)navigationAction decisionHandler:(void (^)(WKNavigationActionPolicy))decisionHandler {
    decisionHandler(WKNavigationActionPolicyAllow);
}

- (void)webView:(WKWebView *)webView didFinishNavigation:(null_unspecified WKNavigation *)navigation {
    NSLog(@"");
}

- (void)observeValueForKeyPath:(nullable NSString *)keyPath ofObject:(nullable id)object change:(nullable NSDictionary<NSKeyValueChangeKey, id> *)change context:(nullable void *)context {
    self.progressView.progress = self.webView.estimatedProgress;
}

@end
```



## 效果

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210616201930.png">

