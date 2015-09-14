---
layout: post
title: "(编写中)iOS崩溃收集与分析，使用plcrashreporter"
description:
headline:
modified: 2015-09-09
category: personal
tags: []
image:
  feature:
comments: true
mathjax:
---

[本文示例代码](https://github.com/everettjf/ios_crash_report_demo)

# 直接调用系统函数获取崩溃时的栈信息

这种方式，能获取到简单的崩溃信息，但无法配合dSYM文件，定位到具体的哪行代码。且能获取到的崩溃类型种类有限，如果要获取更多的信息还需要更多的工作（下文中的开源的plcrashreporter已经做好了）。

- signal 进行错误信号的捕获
- NSSetUncaughtExceptionHandler 未捕获的OC异常

{% highlight c %}

static int s_fatal_signals[] = {
    SIGABRT,
    SIGBUS,
    SIGFPE,
    SIGILL,
    SIGSEGV,
    SIGTRAP,
    SIGTERM,
    SIGKILL,
};


static int s_fatal_signal_num = sizeof(s_fatal_signals) / sizeof(s_fatal_signals[0]);

void UncaughtExceptionHandler(NSException *exception) {
    NSArray *arr = [exception callStackSymbols];//得到当前调用栈信息
    NSString *reason = [exception reason];//非常重要，就是崩溃的原因
    NSString *name = [exception name];//异常类型
}

void SignalHandler(int code)
{
    NSLog(@"signal handler = %d",code);
}

void InitCrashReport()
{
    // 1 linux错误信号捕获
    for (int i = 0; i < s_fatal_signal_num; ++i) {
        signal(s_fatal_signals[i], SignalHandler);
    }
    
    // 2 objective-c未捕获异常的捕获
    NSSetUncaughtExceptionHandler(&UncaughtExceptionHandler);
}
int main(int argc, char * argv[]) {
    @autoreleasepool {
        InitCrashReport();

        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));
    }
}

{% endhighlight %}

# 使用PLCrashReporter

## 官网 
https://www.plcrashreporter.org/

## 安装
可使用CocoaPods安装：
```
pod 'PLCrashReporter', '~> 1.2'
```

## 示例
{% highlight c %}

//
 // Called to handle a pending crash report.
 //
- (void) handleCrashReport {
     PLCrashReporter *crashReporter = [PLCrashReporter sharedReporter];
     NSData *crashData;
     NSError *error;

     // Try loading the crash report
     crashData = [crashReporter loadPendingCrashReportDataAndReturnError: &error];
     if (crashData == nil) {
         NSLog(@"Could not load crash report: %@", error);
         [crashReporter purgePendingCrashReport];
         return;
     }
    
    [crashData writeToFile:[self crashDataPath] atomically:YES];

     // We could send the report from here, but we'll just print out
     // some debugging info instead
     PLCrashReport *report = [[PLCrashReport alloc] initWithData: crashData error: &error];
     if (report == nil) {
         NSLog(@"Could not parse crash report");
         [crashReporter purgePendingCrashReport];
         return;
     }

     NSLog(@"Crashed on %@", report.systemInfo.timestamp);
     NSLog(@"Crashed with signal %@ (code %@, address=0x%" PRIx64 ")", report.signalInfo.name,
           report.signalInfo.code, report.signalInfo.address);
    
    NSString *humanText = [PLCrashReportTextFormatter stringValueForCrashReport:report withTextFormat:PLCrashReportTextFormatiOS];
    
    [self WriteContent:humanText];
    
     // Purge the report
     [crashReporter purgePendingCrashReport];
    
     return;
 }

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    PLCrashReporter *crashReporter = [PLCrashReporter sharedReporter];
    NSError *error;
    
    // Check if we previously crashed
    if ([crashReporter hasPendingCrashReport])
        [self handleCrashReport];

    // Enable the Crash Reporter
    if (![crashReporter enableCrashReporterAndReturnError: &error])
        NSLog(@"Warning: Could not enable crash reporter: %@", error);
    
    return YES;
}

{% endhighlight %}

## 配合dSYM文件
```
     crashData = [crashReporter loadPendingCrashReportDataAndReturnError: &error];
```
返回的NSData是plcrashreporter私有的格式，通过官方提供的```plcrashutil```工具可转换为标准的苹果崩溃日志。






# PLCrashReporter原理
// TODO

# 其他开源项目
- KSCrash
  https://github.com/kstenerud/KSCrash




