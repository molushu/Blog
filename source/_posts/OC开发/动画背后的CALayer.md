---

title: 动画背后的CALayer
date: 2021-06-19 18:05:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/7AA4D0E0-2FCD-48E3-90EF-0E4E3182978F.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/B82D644D-4560-46D0-87CB-0364162EDD5F.png">



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
        
        self.deleteButton.layer.cornerRadius = 10;
        self.deleteButton.layer.masksToBounds = YES;
        
        self.deleteButton.layer.borderColor = [UIColor lightGrayColor].CGColor;
        self.deleteButton.layer.borderWidth = 2;
        
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



## 效果 

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210619181728.png">
