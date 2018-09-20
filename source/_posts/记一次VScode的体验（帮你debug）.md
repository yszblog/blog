---
title: 记一次VScode的体验（帮你debug）
date: 2018-09-20 13:10:05
tags: [工具]
categories: [Javascript]
description:
  - 偶然发现VScode的提示具有debug的功能
---

### 背景
最近项目刚上线，正在改需求，项目中用到了Vue，elementUI，但是里面有个组件用户不是很会用，选择的方式有点太奇葩，项目经理说要自己弄一个组件（如下图，左侧框架自带的，右侧是自己弄的）
<div style="display: flex;">
<img src="/picture/框架自带控件.png" alt="框架自带控件">
<img src="/picture/自定义控件.png" alt="自定义控件">
</div>
`如上图所示，框架自带的是两个时间一起选。自己搞的是一个一个选，see.这样子傻子都能会用了，妈妈再也不用担心......em......`

### 起因
为什么说人家`VScode`能帮咱`debug`呢？？？写组件的时候掉进个坑。说大不大说小不小，大概这么大吧：😵😵😵
![](/picture/坑.jpg "💩💩💩")
虽说写代码（bug）最重要的是开心，但是我还是深深的陷进去了....久久不能自拔....💀💀
废话不多说，上图！！！
<div style="display: flex;">
<img src="/picture/修改前-this指向不对.png" alt="this指向不对">
<img src="/picture/报错信息.png" alt="报错信息">
</div>
`左侧是代码，右侧是报错信息，万恶的undefined....`

为什么找不到呢？在data中我明明定义了却是undefined?这时候其实我已经猜到可能是this的问题了，但是我不说🙊🙊，我想再游一会~💩💩找找这汤为何在这里
anyway！我最终还是忍臭负屎通过`VScode`碰巧找到了这坑[金汁儿](https://baike.baidu.com/item/%E9%87%91%E6%B1%81/98195?fr=aladdin)为何在这里。
当我鼠标🖱放到`this`关键字的的时候，呦呵，下面就是见证刘谦的...啊呸！见证奇迹的时刻！！
![](/picture/显示错误this.png "")
我的天？this指向出来了？？？  unbelievable！ amazing！！ we are 伐...呸！！！

### 洗白白
知道了为什么就好说了
刚从[金汁儿](https://baike.baidu.com/item/%E9%87%91%E6%B1%81/98195?fr=aladdin)里出来，意犹未尽...
着手咔咔三下五除二就洗白净儿的~
话不多说，开洗
![](/picture/修改后-this指向vue.png "")
套你猴子的！我是谁啊！？啊？！敢敢单单！！是不是白白净净的！一点臭味都没有~this指向改变了~~
箭头函数万岁！超大凉万岁！！夹竹桃天下第一！！！
天佑阿拉德~~~

### 总结
1. elementUI中的组件`DateTimePicker 日期时间选择器`、`Picker Options选项`接收的参数是class（类），其中this的指向是其本身
2. 箭头函数不存在this问题，this指向改变为被调用函数最近的对象，即Vue

Ps：本文其实就是this指向的问题，单独拿出来可能就没这问题了，主要是在Vue里面写惯了this、自然而然的以为this指向的全都是Vue。