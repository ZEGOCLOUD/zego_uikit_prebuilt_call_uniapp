# 快速开始

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

2. 创建自定义基座，填入 AppID。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/47d08e1b29.png" alt="run_with_custom.png"/>

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/02f56f8dad.png" alt="config_custom.png"/>

> 注意：IOS 需要苹果开发者证书。为方便测试，可以暂时只勾选安卓端。

3. 将插件市场的 [ZEGO 即构实时音视频 SDK](https://ext.dcloud.net.cn/plugin?id=3617) SDK 引入到项目中，并找到 manifest.json 中的 App 原生插件配置。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/fc005e6051.png" alt="free_buy_for_cloud_build.png"/>

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/65c125a799.png" alt="choose_native_plugins.png" />

勾选上面购买的 ZEGO 即构实时音视频 SDK 并确认。
<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/2a4289a346.png" alt="check_and_confirm.png" />

4. 将插件市场的 [ZEGOUIKitPrebuiltCall 插件](https://ext.dcloud.net.cn/plugin?id=19688) 下载并导入 HBuilderX。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/8fbac5726a.png" alt="download_and_import.png"/>

由于 zego-PrebuiltCall 中包含了 zego-UIKitCore，因此，导入完成后，你的 uni_modules 会包含两个插件。

<img src="https://media-resource.spreading.io/docuo/workspace564/27e54a759d23575969552654cb45bf89/84e2c5cda7.png" alt="imported.png"/>

5. 在业务页面中引入插件。

在 vue 的 js 部分引用 zego-PrebuiltCall 带 ui 组件，并引入 zego-UIKitCore 部分配置。
```js
import keyCenter from "@/common/KeyCenter";
import ZegoUIKitPrebuiltCall from "@/uni_modules/zego-PrebuiltCall/components/ZegoUIKitPrebuiltCall.nvue"
import { ZegoUIKitPrebuiltCallConfig } from "@/uni_modules/zego-PrebuiltCall"
import { ZegoLayoutMode, ZegoViewPosition } from "@/uni_modules/zego-UIKitCore";

const appID = ref(keyCenter.getAppID());
const appSign = ref(keyCenter.getAppSign());
const userID = ref(keyCenter.getUserID());
const userName = ref(keyCenter.getUserID() + '_Nick');
const callID = ref(keyCenter.getCallID());

const config: ZegoUIKitPrebuiltCallConfig = {
    ...ZegoUIKitPrebuiltCallConfig.oneOnOneVideoCall(), // 预设配置
    audioVideoViewConfig: {
        showMicrophoneStateOnView: true, // 显示麦克风状态
        showCameraStateOnView: true, // 显示摄像头状态
        showUserNameOnView: false, // 不要显示用户名
        showSoundWavesInAudioMode: false, // 关闭摄像头时, 头像四周不要显示声浪
    },
    turnOnCameraWhenJoining: true,
    turnOnMicrophoneWhenJoining: false,
    useSpeakerWhenJoining: true,
    layout: {
        mode: ZegoLayoutMode.PictureInPicture, // 画中画布局
        config: {
            smallViewPosition: ZegoViewPosition.TopLeft, // 小的视图显示在左上角
            switchLargeOrSmallViewByClick: true, // 点击小图会交换大小视图的画面
            smallViewSize: { width: 100, height: 180 }, // 设置小视图的尺寸
            smallViewBackgroundColor: '#007fff', // 蓝色
            largeViewBackgroundColor: '#ff7b00', // 橙色
        }
    },
    onHangUp: () => {
        // 挂断后返回上一页
        uni.navigateBack()
    },
};
```

在 vue 的 template 中使用 zego-PrebuiltCall 带 ui 组件，并将配置传入组件。
```vue
<template>
    <ZegoUIKitPrebuiltCall :appID="appID" :callID="callID" :appSign="appSign" :userID="userID" :userName="userName"
        :config="config">
    </ZegoUIKitPrebuiltCall>
</template>
```

6. 配置入口与页面路由

根据业务场景为通话页配置入口。
```vue
<template>
    <view v-for="item in list" :key="item.name" @click="navigateTo(item.url)">
        {{ item.name }}
    </view>
</template>
<script lang="ts" setup>
const list = [
    {
        name: "基础通话",
        url: "/pages/base-call/index",
    },
]
const navigateTo = (url: string) => {
    uni.navigateTo({
        url
    })
}
</script>
```

打开 pages.json，添加 pages 配置
```json
{
	"pages": [
        // 新增基础通话页
		{
		    "path": "pages/base-call/index",
		    "style": {
		        "navigationBarTitleText": "基础通话"
		    }
		}
	],
}
```

## 运行和测试

至此，您已经完成了所有步骤！

只需在 HBuilderX 中点击**运行到手机或模拟器**，选择需要运行的端侧与基座，即可在设备上运行和测试您的应用程序。

## 常见问题

[如何处理接入错误](https://doc-zh.zego.im/faq?product=Call_Kit&platform=uni-app)
