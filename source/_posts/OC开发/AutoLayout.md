---

title: AutoLayout
date: 2021-08-01 21:54:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801220014.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801222431.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801222937.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801223250.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801223436.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801223658.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801223915.png">



GTVideoToolbar.h

```objective-c
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

#define GTVideoToolbarHeight 60

@interface GTVideoToolbar : UIView
- (void)layoutWithModel:(id)model;
@end

NS_ASSUME_NONNULL_END
```



GTVideoToolbar.m

```objective-c
#import "GTVideoToolbar.h"

@interface GTVideoToolbar()

@property(nonatomic, strong, readwrite) UIImageView *avatorImageView;
@property(nonatomic, strong, readwrite) UILabel *nickLabel;

@property(nonatomic, strong, readwrite) UIImageView *commentImageView;
@property(nonatomic, strong, readwrite) UILabel *commentLabel;

@property(nonatomic, strong, readwrite) UIImageView *likeImageView;
@property(nonatomic, strong, readwrite) UILabel *likeLabel;

@property(nonatomic, strong, readwrite) UIImageView *shareImageView;
@property(nonatomic, strong, readwrite) UILabel *shareLabel;

@end

@implementation GTVideoToolbar

- (instancetype) initWithFrame:(CGRect)frame {
    self = [super initWithFrame:frame];
    if (self) {
        self.backgroundColor = [UIColor whiteColor];
        
        _avatorImageView = [[UIImageView alloc] initWithFrame:CGRectZero];
        _avatorImageView.layer.masksToBounds = YES;
        _avatorImageView.layer.cornerRadius = 15;
        _avatorImageView.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_avatorImageView];
        
        _nickLabel = [[UILabel alloc] init];
        _nickLabel.font = [UIFont systemFontOfSize:15];
        _nickLabel.textColor = [UIColor lightGrayColor];
        _nickLabel.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_nickLabel];
        
        _commentImageView = [[UIImageView alloc] initWithFrame:CGRectZero];
        _commentImageView.layer.masksToBounds = YES;
        _commentImageView.layer.cornerRadius = 15;
        _commentImageView.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_commentImageView];
        
        _commentLabel = [[UILabel alloc] init];
        _commentLabel.font = [UIFont systemFontOfSize:15];
        _commentLabel.textColor = [UIColor lightGrayColor];
        _commentLabel.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_commentLabel];
        
        _likeImageView = [[UIImageView alloc] initWithFrame:CGRectZero];
        _likeImageView.layer.masksToBounds = YES;
        _likeImageView.layer.cornerRadius = 15;
        _likeImageView.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_likeImageView];
        
        _likeLabel = [[UILabel alloc] init];
        _likeLabel.font = [UIFont systemFontOfSize:15];
        _likeLabel.textColor = [UIColor lightGrayColor];
        _likeLabel.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_likeLabel];
        
        _shareImageView = [[UIImageView alloc] initWithFrame:CGRectZero];
        _shareImageView.layer.masksToBounds = YES;
        _shareImageView.layer.cornerRadius = 15;
        _shareImageView.translatesAutoresizingMaskIntoConstraints = NO;
        _shareImageView.contentMode = UIViewContentModeScaleToFill;
        [self addSubview:_shareImageView];
        
        _shareLabel = [[UILabel alloc] init];
        _shareLabel.font = [UIFont systemFontOfSize:15];
        _shareLabel.textColor = [UIColor lightGrayColor];
        _shareLabel.translatesAutoresizingMaskIntoConstraints = NO;
        [self addSubview:_shareLabel];
    }
    
    return self;
}

- (void)layoutWithModel:(id)model {
    _avatorImageView.image = [UIImage imageNamed:@"icon.bundle/icon.png"];
    _nickLabel.text = @"极客时间";
    
    _commentImageView.image = [UIImage imageNamed:@"icon.bundle/page@2x.png"];
    _commentLabel.text = @"100";

    _likeImageView.image = [UIImage imageNamed:@"icon.bundle/like@2x.png"];
    _likeLabel.text = @"25";

    _shareImageView.image = [UIImage imageNamed:@"icon.bundle/video@2x.png"];
    _shareLabel.text = @"分享";
    
    [NSLayoutConstraint activateConstraints:@[
        [NSLayoutConstraint constraintWithItem:_avatorImageView
                                    attribute:NSLayoutAttributeCenterY
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:self
                                    attribute:NSLayoutAttributeCenterY
                                    multiplier:1
                                    constant:0],
        
        [NSLayoutConstraint constraintWithItem:_avatorImageView
                                    attribute:NSLayoutAttributeLeft
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:self
                                    attribute:NSLayoutAttributeLeft
                                    multiplier:1
                                    constant:15],
        
        [NSLayoutConstraint constraintWithItem:_avatorImageView
                                    attribute:NSLayoutAttributeWidth
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:nil
                                    attribute:NSLayoutAttributeNotAnAttribute
                                    multiplier:1
                                    constant:30],
        
        [NSLayoutConstraint constraintWithItem:_avatorImageView
                                    attribute:NSLayoutAttributeHeight
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:nil
                                    attribute:NSLayoutAttributeNotAnAttribute
                                    multiplier:1
                                    constant:30],
        
        [NSLayoutConstraint constraintWithItem:_nickLabel
                                    attribute:NSLayoutAttributeCenterY
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:_avatorImageView
                                    attribute:NSLayoutAttributeCenterY
                                    multiplier:1
                                    constant:0],
        
        [NSLayoutConstraint constraintWithItem:_nickLabel
                                    attribute:NSLayoutAttributeLeft
                                    relatedBy:NSLayoutRelationEqual
                                    toItem:_avatorImageView
                                    attribute:NSLayoutAttributeRight
                                    multiplier:1
                                    constant:0],
    ]];
    
    NSString *vflString =  @"H:|-15-[_avatorImageView]-0-[_nickLabel]->=0-[_commentImageView(==_avatorImageView)]-0-[_commentLabel]-15-[_likeImageView(==_avatorImageView)]-0-[_likeLabel]-15-[_shareImageView(==_avatorImageView)]-0-[_shareLabel]-15-|";
    
    [NSLayoutConstraint activateConstraints:[NSLayoutConstraint constraintsWithVisualFormat:vflString options:NSLayoutFormatAlignAllCenterY metrics:nil views:NSDictionaryOfVariableBindings(_avatorImageView, _nickLabel, _commentImageView, _commentLabel, _likeImageView, _likeLabel, _shareImageView, _shareLabel)]];
    
}

@end  
```



## 效果

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210801224529.png">

