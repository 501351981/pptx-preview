# pptx-preview
纯前端实现的pptx.js文件的预览库，支持npm方式安装，支持ES Module方式引入。

[在线演示](https://501351981.github.io/pptx-preview/examples/dist/)


# 使用

## 下载

```shell
npm i pptx-preview
```

## 使用示例

```javascript
import {init} from 'pptx-preview'

//调用库的init方法生成一个预览器
let pptxPrviewer = init(document.getElementById('pptx-wrapper'), {
    width: 960,
    height: 540
})

//获取文件或者读取文件，获取文件的 ArrayBuffer格式数据，传给组件进行预览
fetch('test.pptx').then(response=>{
    return response.arrayBuffer()
}).then(res =>{
    //调用预览器的preview方法
    pptxPrviewer.preview(res)
})
```

# 关于授权

- 本项目发布的npm包可免费使用，自用商用均可
- 本项目的源码仅供个人学习使用，不得发布到互联网平台中，不得直接修改源码并转为自有项目进行开源

# 支持作者

开发这样一个复杂的预览库，需要投入很多的个人时间，作者经常在周末、节假日进行该项目的开发，付出很多精力，如果该项目帮到了您，还请您不吝打赏。

![](https://501351981.github.io/pptx-preview/examples/dist/wx.png)


- 为什么没有开放源码

我们都知道，如果一件事情没有收益，那是很难长久的，特别是对于一个大龄程序员来说，花费大量的时间"用爱发电"对大家来说是非常值得尊敬的，而我感觉对家庭来说可能是不道德的，没有收益，没有正反馈，很难把这个库完善下去，我们也看到了，很多开源库已经多年没有更新了。

为了更好地实现pptx文件预览的各种细节，本项目需要大家的支持，源码需付费向作者索要，打赏用户（无论多少）均可添加作者微信，交流该库或者前端领域话题。


当然了，也感谢各位大佬的点赞~~