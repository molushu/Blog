---

title: UIButton
date: 2021-06-15 20:11:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/5100741F-1299-402E-8590-3A3361DBF8BF.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210615213933.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210615214158.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210615214423.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/71BB2145-BE32-4DC9-884F-3A96BFC98C58.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210615215142.png">



GTNormalTableViewCell.h

```objective-c
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface GTNormalTableViewCell : UITableViewCell

- (void)layoutTableViewCell;

@end

NS_ASSUME_NONNULL_END
```



GTNormalTableViewCell.m

```objective-c
#import "GTNormalTableViewCell.h"

@interface GTNormalTableViewCell()

@property(nonatomic, strong, readwrite) UILabel *titleLabel;
@property(nonatomic, strong, readwrite) UILabel *sourceLabel;
@property(nonatomic, strong, readwrite) UILabel *commentLabel;
@property(nonatomic, strong, readwrite) UILabel *timeLabel;

@property(nonatomic, strong, readwrite) UIImageView *rightImageView;
@property(nonatomic, strong, readwrite) UIButton *deleteButton;

@end

@implementation GTNormalTableViewCell

- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(nullable NSString *)reuseIdentifier {
    self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];
    if (self) {
        self.titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(20, 15, 300, 50)];
//        self.titleLabel.backgroundColor = [UIColor redColor];
        self.titleLabel.font = [UIFont systemFontOfSize:16];
        self.titleLabel.textColor = [UIColor blackColor];
        [self.contentView addSubview:_titleLabel];
        
        self.sourceLabel = [[UILabel alloc] initWithFrame:CGRectMake(20, 80, 0, 0)];
//        self.sourceLabel.backgroundColor = [UIColor redColor];
        self.sourceLabel.font = [UIFont systemFontOfSize:12];
        self.sourceLabel.textColor = [UIColor grayColor];
        [self.contentView addSubview:_sourceLabel];
        
        self.commentLabel = [[UILabel alloc] initWithFrame:CGRectMake(0, 80, 0, 0)];
//        self.commentLabel.backgroundColor = [UIColor redColor];
        self.commentLabel.font = [UIFont systemFontOfSize:12];
        self.commentLabel.textColor = [UIColor grayColor];
        [self.contentView addSubview:_commentLabel];
        
        self.timeLabel = [[UILabel alloc] initWithFrame:CGRectMake(0, 80, 0, 0)];
//        self.timeLabel.backgroundColor = [UIColor redColor];
        self.timeLabel.font = [UIFont systemFontOfSize:12];
        self.timeLabel.textColor = [UIColor grayColor];
        [self.contentView addSubview:_timeLabel];
        
        self.rightImageView = [[UIImageView alloc] initWithFrame:CGRectMake(300, 15, 70, 70)];
        self.rightImageView.backgroundColor = [UIColor redColor];
        self.rightImageView.contentMode = UIViewContentModeScaleAspectFit;
        [self.contentView addSubview:_rightImageView];
        
        self.deleteButton = [[UIButton alloc] initWithFrame:CGRectMake(250, 80, 30, 20)];
        [self.deleteButton setTitle:@"X" forState:UIControlStateNormal];
        [self.deleteButton setTitle:@"V" forState:UIControlStateHighlighted];
        [self.deleteButton addTarget:self action:@selector(deleteButtonClick) forControlEvents:UIControlEventTouchUpInside];
        self.deleteButton.backgroundColor = [UIColor blueColor];
        [self.contentView addSubview:_deleteButton];
        
    }
    return self;
}

- (void)layoutTableViewCell {
    self.titleLabel.text = @"极客时间IOS开发";
    
    self.sourceLabel.text = @"极客时间";
    [self.sourceLabel sizeToFit];
    
    self.commentLabel.text = @"1888评论";
    [self.commentLabel sizeToFit];
    self.commentLabel.frame = CGRectMake(self.sourceLabel.frame.origin.x + self.sourceLabel.frame.size.width + 15, self.commentLabel.frame.origin.y, self.commentLabel.frame.size.width, self.commentLabel.frame.size.height);
    
    self.timeLabel.text = @"三分钟前";
    [self.timeLabel sizeToFit];
    self.timeLabel.frame = CGRectMake(self.commentLabel.frame.origin.x + self.commentLabel.frame.size.width + 15, self.timeLabel.frame.origin.y, self.timeLabel.frame.size.width, self.timeLabel.frame.size.height);
    
    self.rightImageView.image = [UIImage imageNamed:@"icon.bundle/icon.png"];
}

- (void)deleteButtonClick {
    NSLog(@"deleteButtonClick");
}

@end
```



ViewController.m

```objective-c
#import "ViewController.h"
#import "GTNormalTableViewCell.h"

@interface ViewController ()<UITableViewDataSource, UITableViewDelegate>

@end

//通过重写UIViewController类中的一些方法，来观察ViewController的生命周期
@implementation ViewController

- (instancetype)init {
    self = [super init];
    if (self) {
        
    }
    return self;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    UITableView *tableView = [[UITableView alloc] initWithFrame:self.view.bounds];
    tableView.dataSource = self;
    tableView.delegate = self;
    [self.view addSubview:tableView];
}

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {
    return 100;
}

- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    UIViewController *controller = [[UIViewController alloc] init];
    controller.title = [NSString stringWithFormat:@"%@", @(indexPath.row)];
    controller.view.backgroundColor = [UIColor whiteColor];
    [self.navigationController pushViewController:controller animated:YES];
}
    
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 20;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    GTNormalTableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"id"];
    if (!cell) {
        cell = [[GTNormalTableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:@"id"];
    }
    
    [cell layoutTableViewCell];
    
    return cell;
}

@end
```



## 效果

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210615215728.png">
