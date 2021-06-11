---

title: UITableView
date: 2021-06-11 15:34:44
categories: 
- OC开发
---

## 1、基本配置展示

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611154706.png">



<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/087678A0-B944-4F36-9720-1210738A088B.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/DC923DA9-5B1A-462B-8343-BFB0730730E2.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611162338.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611162952.png">

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611163324.png">

```objective-c
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
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"id"];
    if (!cell) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:@"id"];
    }
    
    cell.textLabel.text = [NSString stringWithFormat:@"主标题 - %@", @(indexPath.row)];
    cell.detailTextLabel.text = @"副标题";
    cell.imageView.image = [UIImage imageNamed:@"icon.bundle/video@2x.png"];
    return cell;
}

@end
```

## 效果：

<img src="https://gitee.com/molushu/blog-gallery-1/raw/master/img/20210611164039.png">
