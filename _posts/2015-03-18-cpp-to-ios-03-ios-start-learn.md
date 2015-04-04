---
layout: post
title: "cpp to ios 03 ios start learn"
description: ""
category:
tags: []
---
{% include JB/setup %}

# 知识点
## GCD (Grand Central Dispatch)
<pre>
dispatch_once
</pre>

## AutoLayout
    * http://www.cocoachina.com/industry/20131203/7462.html
    * http://www.cnblogs.com/zer0Black/p/3977288.html
    * 按住？多选，然后Editor\Pin\...（?或command都可以多选，不知道有什么区别）

## Assistant Editor
    * option+command+return
    * 选中控件，按住ctrl，拖拽到右侧代码中（@interface下或@implementation下）

## 静态库
编码完成之后，直接Run就能成功生成Framework文件了，选择 xCode->Window->Organizer->Projects->Your Project, 打开工程的Derived Data目录，这样就能找到生成的Framework文件了

---

# 第三方
## AFNetworking
## MBProgressHUD
## GDataXMLParser
## GrowingTextView
## SlideSwitch
## MWPhotoBrowser
## MMPlaceHolder
    https://github.com/adad184/MMPlaceHolder
## Masonry
    http://adad184.com/2014/09/28/use-masonry-to-quick-solve-autolayout/
    https://github.com/Masonry/Masonry

---

# 代码片段

## TextField设置高度
修改border为无边框


## Contraints
multiplier 作用于第二个参数（设置为0.5，1，1.5）


## 汇总
<pre>
// UIScreen
[[UIScreen mainScreen] bounds]];

// CGRect
CGRect *rect = CGRectMake(0,0,100,100);
self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];

// UIColor
[UIColor whiteColor];
[UIColor colorWithRed:1 green:0 blue:0 alpha:1];
[UIColor colorWithPatternImage:backImage];


// Layer - 圆角Button或TextField
self.buttonLogon.layer.cornerRadius = self.buttonLogon.bounds.size.height / 2;
self.buttonLogon.layer.masksToBounds = YES;

// UIWindow
self.window.backgroundColor = [UIColor redColor];
[self.window makeKeyAndVisible];

// UIImage (from resource)
UIImage *backImage = [UIImage imageNamed:@"background"];

// UIView
UIView *myView = [[UIView alloc] initWithFrame:CGRectMake(.....)];
[self.window addSubView:myView];

// UIApplication
// 隐藏状态栏
//[[UIApplication sharedApplication] setStatusBarHidden:TRUE];

// NSBundle
// ...

// rootViewController - UIViewController
MyFirstViewController *viewController = [[MyFirstViewController alloc] initWithNibName:nil bundle:nil];

//在setRootViewController里会自动帮我们把viewController.view 添加到 self.window 上
self.window.rootViewController = viewController;

// UIFont
// label.font = [UIFont systemFontOfSize:60];


// UIButton
[textFieldButton addTarget:self action:@selector(onTextFieldButtonClicked:) forControlEvents:UIControlEventTouchUpInside];
- (void)onTextFieldButtonClicked:(UIButton*)button{
}


// 导航
// push
// push - pop
- (void)pushuToVC:(UIButton*)btn{
    //这里使用导航方式跳转到LLViewController
    LLViewController *viewController = [[LLViewController alloc] init];
    [self.navigationController pushViewController:viewController animated:YES];
}
    //由于是push过来的，这里使用pop方式导航回去
    // push的目标View返回
    [self.navigationController popViewControllerAnimated:YES];


// modal
// present - dismiss
- (void)presentVC:(UIButton*)btn{
    //这里使用展示方式跳转到LLViewController
    MMViewController *viewController = [[MMViewController alloc] init];
    [self presentViewController:viewController animated:YES completion:^{

    }];
}
    //由于是present过来的，这里使用dismiss方式回去
    [self dismissViewControllerAnimated:YES completion:^{

    }];




</pre>

## 代码写界面
<pre>
// controller 中用这个
CGRect frame = [self.view bounds];

// delegate中用这个
[[UIScreen mainScreen] bounds]];

</pre>

## json
<pre>
    NSString *url = @"http://xx.x.x.x";
    NSURLRequest *request = [NSURLRequest requestWithURL:[NSURL URLWithString:url]];
    NSData *response = [NSURLConnection sendSynchronousRequest:request returningResponse:nil error:nil];
    NSDictionary *dict = [NSJSONSerialization JSONObjectWithData:response options:NSJSONReadingMutableLeaves error:nil];

</pre>

## AFNetworking
