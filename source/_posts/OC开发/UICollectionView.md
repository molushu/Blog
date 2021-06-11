---

title: UICollectionView
date: 2021-06-11 22:42:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/B0CEA172-E88E-4C3F-85C8-50939FCB0C9B.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611225419.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611230002.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/DDD5AA7F-56BB-4ED6-A562-3385BB6442A5.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/84D12152-04A0-4E77-A098-81E160A9DD40.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611231251.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611231509.png">



```objective-c
#import "GTVideoViewController.h"

@interface GTVideoViewController () <UICollectionViewDelegate, UICollectionViewDataSource>

@end

@implementation GTVideoViewController

- (instancetype) init {
    self = [super init];
    if (self) {
        self.tabBarItem.title = @"视频";
        self.tabBarItem.image = [UIImage imageNamed:@"icon.bundle/video@2x.png"];
        self.tabBarItem.selectedImage = [UIImage imageNamed:@"icon.bundle/video_selected@2x.png"];
    }
    return self;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    UICollectionViewFlowLayout *flowLayout = [[UICollectionViewFlowLayout alloc] init];
    flowLayout.minimumLineSpacing = 10;
    flowLayout.minimumInteritemSpacing = 10;
    flowLayout.itemSize = CGSizeMake((self.view.frame.size.width - 10) / 2, 300);
    
    UICollectionView *collectionView = [[UICollectionView alloc] initWithFrame:self.view.bounds collectionViewLayout:flowLayout];
    
    collectionView.delegate = self;
    collectionView.dataSource = self;
    
    //根据ReuseIdentifier注册cell类型
    [collectionView registerClass:[UICollectionViewCell class] forCellWithReuseIdentifier:@"UICollectionViewCell"];
    
    [self.view addSubview:collectionView];
}

- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section {
    return 20;
}

- (__kindof UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath {
    //如果系统的复用回收池中没有，会在上述注册的ReuseIdentifier自动创建一个cell
    UICollectionViewCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"UICollectionViewCell" forIndexPath:indexPath];
    cell.backgroundColor = [UIColor redColor];
    
    return cell;
}

/*
     UICollectionViewDelegateFlowLayout是继承自UICollectionViewDelegate，当我们设置了
     collectionView的layout为UICollectionViewFlowLayout，设置collectionView的delegate
     就可以实现UICollectionViewDelegateFlowLayout中的方法了
 */
- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath {
    if (indexPath.item % 3 == 0) {
        return CGSizeMake(self.view.frame.size.width, 100);
    } else {
        return CGSizeMake((self.view.frame.size.width - 10) / 2, 300);
    }
}

@end

```

## 效果：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611232102.png">
