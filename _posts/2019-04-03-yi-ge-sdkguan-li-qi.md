---
layout: post
title: "一个SDK管理器"
date: 2019-04-03 16:52:40 +0800
modified_date: 2019-04-13 22:45:53 +0800
categories: Programming
tags: sdk
---

游戏若要在[渠道](http://gamerank.sfw.cn/)上架，通常需要接入渠道方提供的SDK，如用户系统、支付系统等等。虽然市面上已有许多打包工具（[AnySDK](http://www.anysdk.com/)，[U8SDK](http://www.6xsdk.com/)）让游戏开发者可以快速接入各个渠道，但是因为不见得所有的渠道都能得到支持，游戏开发者仍然需要自己去设计代码架构，可以更方便地接入SDK。

我自己用TypeScript写了一个简易的SDK管理器。它肯定是丑陋并且不完善的，但是至少提供了一个原型；它与具体的游戏逻辑分离，又可以适当扩展；这样，当我下一次开始新项目的时候就不需要[重复造轮子](https://zh.wikipedia.org/wiki/%E9%87%8D%E9%80%A0%E8%BD%AE%E5%AD%90)了。

## 设计

单例类`SDKManager`负责管理所有SDK插件。用户通过`getUserPlugin()`、`getIAPPlugin()`方法获取用户插件、支付插件。

```typescript
SDKManager.getInstance().getUserPlugin().login((code, msg) => {
    // ...
});

SDKManager.getInstance().getIAPPlugin().payForProduct(productInfo, (code, msg) => {
    // ...
});
```

接入渠道SDK的时候，需要按需求继承`UserPlugin`、`IAPPlugin`等等，并重写它们的方法。

在游戏启动之后的适当时机，执行以下代码完成初始化：

```typescript
const manager = SDKManager.getInstance();
manager.setChannel(999);
manager.init();
manager.loadAllPlugins();
```

## 部分实现

```typescript
/**
 * 渠道代理，每个渠道应当继承ChannelAgent
 */
export class ChannelAgent {
    /**
     * Override this.
     * 通常是在这个方法里加载渠道的库
     */
    public init() {

    }

    /**
     * Override this.
     * 渠道代理自己决定要注册哪些插件
     */
    public loadAllPlugins() {
        SDKManager.getInstance().registerUserPlugin(new UserPlugin);
        SDKManager.getInstance().registerIAPPlugin(new IAPPlugin);
    }
}

export class SDKManager {
    private userPlugin: UserPlugin;                                  // 用户插件
    // Other plugins...

    private currentChannelID: ChannelID = ChannelID.NONE;            // 当前渠道ID

    private agent: ChannelAgent;                                     // 渠道代理，每个渠道应当继承ChannelAgent

    /**
     * 设置当前渠道
     */
    public setChannel(id: ChannelID) {
        this.currentChannelID = id;
    }

    public init() {
        switch (this.currentChannelID) {                             // 根据当前渠道ID，选择加载对应的代理
            case ChannelID.QUICK: 
                {
                    const m = require('./registers/RegisterQuick');
                    this.agent = new m.QuickAgent();    
                }   
                break;
            // Other channels...

            default:
                console.log(`WARNING: no channel`);
                this.agent = new ChannelAgent();
                break;
        }

        this.agent.init();
    }

    /**
     * 加载所有插件
     */
    public loadAllPlugins() {
        this.agent.loadAllPlugins();
    }

    public getUserPlugin(): UserPlugin {
        return this.userPlugin;
    }
}

export class UserPlugin {

    /**
     * Override this
     */
    public login(callback?: (code: UserActionResultCode, msg: any) => void) {
        
    }

    // Other methods...
}
```

假设现在要接入一个名为Foo的渠道，可以创建一个脚本`registers/RegisterFoo.ts`，代码内容如下：

```typescript
export class FooAgent extends ChannelAgent {

    public init() {
        // 加载Foo提供的代码库
    }

    public loadAllPlugins() {
        SDKManager.getInstance().registerUserPlugin(new FooUserPlugin);
        SDKManager.getInstance().registerIAPPlugin(new FooIAPPlugin);
    }
}

export class FooUserPlugin extends UserPlugin {
    // ...
}

export class FooIAPPlugin extends IAPPlugin {
    // ...
}
```

最后别忘了修改`SDKManager`的`init`方法，插入：

```typescript
case ChannelID.FOO: 
    {
        const m = require('./registers/RegisterFoo');
        this.agent = new m.FooAgent();    
    }   
    break;
```

## 全部代码

见仓库[XDSDK](https://github.com/alxdhuang/XDSDK)。
