## 概要 ##

DoubanAPICocoa是一个Cocoa封装的豆瓣API库，非官方版，可以使用于iOS，并支持iOS6及之后的版本。[OS X 版本可参考这里](https://github.com/GuoJing/DoubanAPICocoa-OSX)

DoubanAPICocoa的底层支持并兼容老版本的[douban-objc-client](https://github.com/lincode/douban-objc-client)，熟悉[douban-objc-client](https://github.com/lincode/douban-objc-client)开发的同学也可以不用更新代码，直接移植到新的库里并且编译通过。但推荐使用DoubanAPICocoa提供的DOUEngine来实现代码。

注意：示例请自行替换apiKey，并且自行申请相关权限，如豆邮和线上活动以及更多高级的功能。

### 目的 ###

1. 使开发更加容易，不用关注网络层的细节

### 特点 ###

1. 封装网络层
2. 简单
3. 使用闭包让开发者开发更简单
3. All consts
3. No Warning, No Error and No Build Analyze Errors

### 样例 ###

#### 验证 ####

声明一个engine：

    engine = [[DOUEngine alloc] initWithApiKey:kAPIKey withSecretKey:kPrivateKey withRedirUrl:kRedirectUrl];

打开豆瓣验证url：

    NSString *url_str = [self.engine getConnectUrl];

从豆瓣返回code并初始化engine：

    [self.engine didLoadWithCode:code];

验证通过。

#### 我是谁 ###

    [u getWhoAmI:successUserBlock failedBlock:failBlock];

#### 发广播 ####
    
    DOUBroadcastEngine *s = [self.engine getEngine:kDOUBroadcast];
    [s say:self.shuo_field.title successBlock:successBlock failedBlock:failBlock];

#### 获取同城活动 ####

    DOUEventEngine *event_engine = [self.engine getEngine:kDOUEvent];
    [event_engine getEventWithRemoteID:self.eid_field.title successBlock:successBlock failedBlock:failedBlock];

### 变量 ###

该库封装了常用的变量，比如发日记如果是发私有的日记，可以直接使用kDOUPrivacyPrivate，同样相册的排序方式可以使用kDOUOrderDesc，无需自己写变量。

常用的变量文件在库的Engine/Utils里。

1. DOUAPIConsts.h
2. DOUAPIConsts.h
3. DOUAPIErrorConsts.h

### 开发 ###

这个库支持最老的底层的实现方法，也可以非常容易的使用engine进行api开发，可以通过kDOU产品线获得相应的engine，每个engine都有getEngine方法。不过推荐在外面包装一个单例的共享engine，方便在代码各处使用。

可以删除任意不需要的模块并重新打包和分发，减少代码。

### 示例 ###

大部分接口都有基本的示例，今后会提供更多更丰富的示例。

## 其他 ##

**[豆瓣API](http://developers.douban.com/)**

**并且该版本不支持GData等V1版本特性，只支持V2。**

如果你需要iOS版本，请去:

1. 开发版：[douban-objc-client](https://github.com/lincode/douban-objc-client)
2. 官方版：[douban-objc-client](https://github.com/douban/douban-objc-client)

## 信息 ##

当前版本V0.1.3，主要职责为兼容iOS版本并且封装网络层，今后使用的方法可能会不同。

当前版本不支持GData等V1版本特性，只支持V2，所以必须使用https。

当前版本只适用于64位版本，考虑到今后32位的Mac也不多，所以暂时不打算支持。

## 使用 ##

### Sample我还在做 ###

### 发起一个异步请求 ###

	NSString *subPath = [NSString stringWithFormat:@"/v2/event/%d", event_id];
	
	DOUQuery *query = [[[DOUQuery alloc] initWithSubPath:subPath parameters:nil] autorelease];

	query.apiBaseUrlString = service.apiBaseUrlString;
	
	DOUHttpRequest *req = [DOUHttpRequest requestWithQuery:query target:self];

	DOUService *service = [DOUService sharedInstance];
	[service addRequest:req];


## 历史 ##

v0.1

1. 发布一个移植版本。

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/GuoJing/doubanapicocoa-ios/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

