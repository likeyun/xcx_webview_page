### xcx_webview_page
微信小程序webview加载页面源码

### 如何使用？

在你小程序的pages目录创建一个h5目录，h5目录里面创建index page，结果如下：

![](https://p0.meituan.net/dpmerchantpic/31e37e136e4e87bf5a6426faa3630d5e13932.jpg%40200w_200h_1e_1l)

然后拷贝以下代码粘贴进pages/h5/index.wxml里面

#### index.wxml
```
<web-view src="{{imgurl}}"></web-view>
```
再拷贝以下代码粘贴进pages/h5/index.js里面

#### index.js

```
Page({
	data: {
		imgurl: '',
	},
	onLoad(options) {
		const imgurl = options.url;
		if(imgurl) {
			this.setData({
				imgurl: imgurl
			})
		}else {
			wx.showModal({
			  title: '请传递图片地址参数',
			})
		}
	},

	/**
	 * 用户点击右上角分享
	 */
	onShareAppMessage() {}
})
```
保存后即可使用。

使用小程序后台生成二维码的工具，按照以下格式生成二维码即可查看页面。

![](https://p0.meituan.net/dpmerchantpic/d952201d90cf210f1edeecc466b88dc054312.jpg%40800w_200h_1e_1l)

### 什么是业务域名下的图片地址？

因为使用了webview组件，因此这个仅限企业认证的小程序使用，
企业认证小程序可以在 `开发管理->开发设置->业务域名`，
进行配置用于在webview组件加载的图片地址，
所以图片地址只允许在业务域名的服务器的图片地址，
因此你不需要担心被他人传递参数滥用你的小程序，
别人无法使用自己服务器的图片地址进行跳转。

![](https://p0.meituan.net/dpmerchantpic/9746440b7c8db3b201e7fd4d1b5cef2118860.jpg%40200w_200h_1e_1l)

配置了业务域名后，在自己的服务器上传一张图片，获取图片地址即可用于生成小程序码和URLScheme，传递的参数是 `url`

### 示例

假设你的业务域名是 `www.baidu.com`，你上传了一张图片到你服务器的 `img` 目录，图片名是`wxqrcode.png`，那么你生成二维码的路径就是：

```
pages/h5/index?utl=https://www.baidu.com/img/wxqrcode.png
```

