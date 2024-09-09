# 音视频通话 UIKit

这份文档将指导您如何在 uni-app 项目集成 `音视频通话 UIKit` uniapp SDK 并快速开始音视频通话。

## 准备环境

在开始集成音视频 UIKit 前，请确保开发环境满足以下要求：

- 参考 [uni-app 文档](https://zh.uniapp.dcloud.io/quickstart-hx.html)创建项目。
- HBuilderX 3.0.0 或以上版本。
- IOS
  - Xcode 15.0 或以上版本。
  - iOS 12.0 或以上版本且支持音视频的 iOS 设备。
- Android
  - Android Studio 2020.3.1 或以上版本。
  - Android SDK 25、Android SDK Build-Tools 25.0.2、Android SDK Platform-Tools 25.x.x 或以上版本。
  - Android 4.4 或以上版本，且支持音视频的 Android 设备。
- 设备已经连接到 Internet。

## 前提条件

- 已在 [ZEGO 控制台](https://console.zego.im) 创建项目，并申请有效的 AppID 和 AppSign，详情请参考 [控制台 - 项目信息](https://doc-zh.zego.im/article/12107)。
- 联系 ZEGO 技术支持，开通 UIKit 相关服务。

## 实现流程

### 引入SDK

1. 使用 HBuilderX 打开 manifest.json，重新生成一个 `uni-app 应用标识`。

2. 在插件市场购买 [ZEGO 即构实时音视频 SDK](https://ext.dcloud.net.cn/plugin?id=3617)。购买时填入的 AppID 必须和后面需要运行的 AppID 一致。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/fc005e6051.png" alt="free_buy_for_cloud_build.png"/>

单击项目目录的 “manifest.json” 文件后，单击 “App 原生插件配置 > 云端插件 [选择云端插件]”。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/65c125a799.png" alt="choose_native_plugins.png" />

在“云端插件选择”弹窗勾选上面购买的 ZEGO 即构实时音视频 SDK 并确认。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/2a4289a346.png" alt="check_and_confirm.png" />

3. 创建自定义基座，填入 AppID。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/47d08e1b29.png" alt="run_with_custom.png"/>

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/02f56f8dad.png" alt="config_custom.png"/>

> 注意：IOS 需要苹果开发者证书。为方便测试，可以暂时只勾选安卓端。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/fc005e6051.png" alt="free_buy_for_cloud_build.png"/>

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/65c125a799.png" alt="choose_native_plugins.png" />

勾选上面购买的 ZEGO 即构实时音视频 SDK 并确认。
<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/2a4289a346.png" alt="check_and_confirm.png" />

4. 将插件市场的 [ZEGOUIKitPrebuiltCall 插件](https://ext.dcloud.net.cn/plugin?id=19688) 下载并导入 HBuilderX。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/8fbac5726a.png" alt="download_and_import.png"/>

由于 zego-PrebuiltCall 中包含了 zego-UIKitCore，因此，导入完成后，您的 uni_modules 会包含以下插件。

<img src="https://media-resource.spreading.io/docuo/workspace733/92cf2c578a7f03194465a905bb923c76/9276069cc7.png" alt="imported.png"/>

## 运行和测试

至此，您已经完成了所有步骤！

只需在 HBuilderX 中点击**运行到手机或模拟器**，选择需要运行的端侧与基座，即可在设备上运行和测试您的应用程序。

## 常见问题

[如何处理接入错误](https://doc-zh.zego.im/faq?product=Call_Kit&platform=uni-app)
