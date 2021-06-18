---

title: protocol
date: 2021-06-18 15:10:44
categories: 
- OC开发
---

## 1、基本配置展示



GTNormalTableViewCell.h

```objective-c
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@protocol GTNormalTableViewCellDelegate <NSObject>

- (void)tableViewCell:(UITableViewCell *)tableViewCell clickDeleteButton:(UIButton *)deleteButton;

@end

@interface GTNormalTableViewCell : UITableViewCell

@property(nonatomic, weak, readwrite) id<GTNormalTableViewCellDelegate> delegate;

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
    if (self.delegate && [self.delegate respondsToSelector:@selector(tableViewCell:clickDeleteButton:)]) {
        [self.delegate tableViewCell:self clickDeleteButton:self.deleteButton];
    }
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

