---

title: UIView动画
date: 2021-06-18 12:30:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/4C36FFBE-D678-4751-8899-13D70627C0FF.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/577C0426-C38C-4CDF-BE42-1DCF3BF52D3F.png">



GTDeleteCellView.h

```objective-c
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface GTDeleteCellView : UIView

- (void)showDeleteViewFromPoint: (CGPoint)point clickBlock:(dispatch_block_t) clickBlock;

@end

NS_ASSUME_NONNULL_END
```



GTDeleteCellView.m

```objective-c
#import "GTDeleteCellView.h"

@interface GTDeleteCellView ()

@property(nonatomic, strong, readwrite) UIView *backgroundView;
@property(nonatomic, strong, readwrite) UIButton *deleteButton;
@property(nonatomic, copy, readwrite) dispatch_block_t deleteBlock;

@end

@implementation GTDeleteCellView

- (instancetype)initWithFrame:(CGRect)frame {
    self = [super initWithFrame:frame];
    if (self) {
        _backgroundView = [[UIView alloc] initWithFrame:self.bounds];
        _backgroundView.backgroundColor = [UIColor blackColor];
        _backgroundView.alpha = 0.5;
        UITapGestureRecognizer *tapGesture = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(dismissDeleteView)];
        [_backgroundView addGestureRecognizer:tapGesture];
        [self addSubview:_backgroundView];
        
        _deleteButton = [[UIButton alloc] initWithFrame:CGRectMake(0, 0, 0, 0)];
        [_deleteButton addTarget:self action:@selector(_clickButton) forControlEvents:UIControlEventTouchUpInside];
        _deleteButton.backgroundColor = [UIColor blueColor];
        [self addSubview:_deleteButton];
    }
    return self;
}

- (void)showDeleteViewFromPoint: (CGPoint)point clickBlock:(dispatch_block_t) clickBlock {
    _deleteButton.frame = CGRectMake(point.x, point.y, 0, 0);
    _deleteBlock = [clickBlock copy];
    
//    [[UIApplication sharedApplication].keyWindow addSubview:self];
    [UIApplication.sharedApplication.windows.lastObject addSubview:self];
    
//    [UIView animateWithDuration:1.f animations:^{
//            self.deleteButton.frame = CGRectMake((self.bounds.size.width - 200) / 2, (self.bounds.size.height - 200) / 2, 200, 200);
//    }];
    
    [UIView animateWithDuration:1.f delay:0.f usingSpringWithDamping:0.5 initialSpringVelocity:0.5 options:UIViewAnimationOptionCurveEaseInOut animations:^{
            self.deleteButton.frame = CGRectMake((self.bounds.size.width - 200) / 2, (self.bounds.size.height - 200) / 2, 200, 200);
        } completion:^(BOOL finished) {
            NSLog(@"");
        }];
}

- (void)dismissDeleteView {
    [self removeFromSuperview];
}

- (void)_clickButton {
    if (_deleteBlock) {
        _deleteBlock();
    }
    [self removeFromSuperview];
}

@end
```

ViewController.m

```objective-c
#import "ViewController.h"
#import "GTNormalTableViewCell.h"
#import "GTDetailViewController.h"
#import "GTDeleteCellView.h"

@interface ViewController ()<UITableViewDataSource, UITableViewDelegate, GTNormalTableViewCellDelegate>

@property(nonatomic, strong, readwrite) UITableView *tableView;
@property(nonatomic, strong, readwrite) NSMutableArray *dataArray;

@end

//通过重写UIViewController类中的一些方法，来观察ViewController的生命周期
@implementation ViewController

- (instancetype)init {
    self = [super init];
    if (self) {
        _dataArray = @[].mutableCopy;
        for (int i = 0; i < 20; i++) {
            [_dataArray addObject:@(i)];
        }
    }
    return self;
}

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    _tableView = [[UITableView alloc] initWithFrame:self.view.bounds];
    _tableView.dataSource = self;
    _tableView.delegate = self;
    [self.view addSubview:_tableView];
}

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {
    return 100;
}

- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    GTDetailViewController *controller = [[GTDetailViewController alloc] init];
    controller.title = [NSString stringWithFormat:@"%@", @(indexPath.row)];
    controller.view.backgroundColor = [UIColor whiteColor];
    [self.navigationController pushViewController:controller animated:YES];
}
    
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return _dataArray.count;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    GTNormalTableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"id"];
    if (!cell) {
        cell = [[GTNormalTableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:@"id"];
        cell.delegate = self;
    }
    
    [cell layoutTableViewCell];
    
    return cell;
}

- (void)tableViewCell:(UITableViewCell *)tableViewCell clickDeleteButton:(UIButton *)deleteButton {
    GTDeleteCellView *deleteView = [[GTDeleteCellView alloc] initWithFrame:self.view.bounds];
    
    CGRect rect = [tableViewCell convertRect:deleteButton.frame toView:nil];
    
    __weak typeof(self) wself = self;
    [deleteView showDeleteViewFromPoint:rect.origin clickBlock:^{
        __strong typeof(self) strongSelf = wself;
        [strongSelf.dataArray removeLastObject];
        [strongSelf.tableView deleteRowsAtIndexPaths:@[[strongSelf.tableView indexPathForCell:tableViewCell]] withRowAnimation:UITableViewRowAnimationAutomatic];
    }];
}

@end
```

