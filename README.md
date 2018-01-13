# wsSearchView
该搜索框组件基于开源项目<a href="https://github.com/icindy/wxSearch">wxSearch</a> 进行了改进，主要有以下几个修改点：
* 增加了注释，修改了一些bug，项目可以跑起来。
* 为了解决搜索框和输入法界面重叠的问题，将搜索组件作为一个独立的页面。
* 修改了界面样式，更加美观。
* 减少了暴露接口，复杂性更低。

下面左图是组件效果图，右边是基于这个组件开发的一个<a href="https://github.com/mindawei/weather">天气预报小程序</a>，扫描二维码可以进行体验。
![wsSearchView效果](screenshoot/wsSearchView.gif)
![查询天气小程序](screenshoot/weahter-weixin.jpg)

# QuickStart
1. 拷贝项目根目录的wxSearchView文件夹到你项目的根目录下（也可以其它位置）。
2. 在你的wxss文件里导入组件的样式（位置为相对位置）：
```
@import "../../wxSearchView/wxSearchView.wxss";
```
3. 在你的wxml文件里导入组件（位置为相对位置）：
```
<include src="../../wxSearchView/wxSearchView.wxml" />
```
4. 在你的js文件里面添加以下代码,主要包括以下5个部分：
* 导入js文件
* 搜索栏初始化
* 转发函数
* 搜索回调函数
* 返回回调函数
```
// 1 导入js文件
var WxSearch = require('../../wxSearchView/wxSearchView.js');

Page({

  data: {},

  
  onLoad: function () {
  
    // 2 搜索栏初始化
    var that = this;
    WxSearch.init(
      that,  // 本页面一个引用
      ['杭州', '嘉兴', "海宁", "桐乡", '宁波', '金华'], // 热点搜索推荐，[]表示不使用
      ['湖北', '湖南', '北京', "南京"],// 搜索匹配，[]表示不使用
      that.mySearchFunction, // 提供一个搜索回调函数
      that.myGobackFunction //提供一个返回回调函数
    );
    
  },

  // 3 转发函数，固定部分，直接拷贝即可
  wxSearchInput: WxSearch.wxSearchInput,  // 输入变化时的操作
  wxSearchKeyTap: WxSearch.wxSearchKeyTap,  // 点击提示或者关键字、历史记录时的操作
  wxSearchDeleteAll: WxSearch.wxSearchDeleteAll, // 删除所有的历史记录
  wxSearchConfirm: WxSearch.wxSearchConfirm,  // 搜索函数
  wxSearchClear: WxSearch.wxSearchClear,  // 清空函数

  // 4 搜索回调函数  
  mySearchFunction: function (value) {
    // do your job here
    // 示例：跳转
    wx.redirectTo({
      url: '../index/index?searchValue='+value
    })
  },

  // 5 返回回调函数
  myGobackFunction: function (value) {
    // do your job here
    // 示例：返回
    wx.redirectTo({
      url: '../index/index?searchValue=返回'  
    })
  }

})
```
