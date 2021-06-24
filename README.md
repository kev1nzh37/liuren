## 前言

昨日摸鱼时，正在回顾`鬼吹灯`小说，每当胡八一提起`十六字阴阳风水秘书`的时候都会激起我想学算命的想法。

<img src="https://img0.baidu.com/it/u=2904036357,912022290&fm=26&fmt=auto&gp=0.jpg"  width="200">

大家看各类影视剧或接头算卦之类的场景时，算命大师一般都会掐指一算，念念有声好似在算着什么，我就很好奇他们是怎么得出结果的？

于是我找到了一种可以随手一算的占卜方式——小六壬。



<img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic2.zhimg.com%2Fv2-dfbfd61ba5aae6928343d104dd9992a9_b.jpg&refer=http%3A%2F%2Fpic2.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1627102913&t=ddfeb472cf0a1438aca1d6638b0579d2"  width="100">

## 占卜方法——小六壬
小六壬也称其为诸葛亮马前课，小六壬的查法:是以大安为起点顺时针查得。按阴历大安起正月顺时针查至你要查的所在月份，再从此月起初一顺时针查至你要查的日子，就知道了日子的好坏。如查时辰，再从此日起子时顺时针查看每个时辰的好坏。例如阴历六月初五辰时；六月为空亡月，初五为赤口日，辰时为留连时。


看起来挺麻烦的，但其实逻辑很简单。我们看下图，几句话你就能明白是怎么算出结果的。

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a2d3c62b33074afdad3e22a3a36f3555~tplv-k3u1fbpfcp-watermark.image)
```javascript
['1.大安','2.留连','3.速喜','4.赤口','5.小吉','6.空亡']
```
结果有6种，分别对应着要占卜的解释。


1. 通过天时地利获取年月日或者随机一个数字。
2. 将数字带入到六个结果中，最终获得占卜的结果。

<img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic1.zhimg.com%2F50%2Fv2-7d608cfddcaf383177defecf67cd44dd_hd.jpg&refer=http%3A%2F%2Fpic1.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1627106438&t=cebc72947601251e944e2f85efac1e2f"  width="200">

下面我们介绍一种方法——活数起课法。

## 活数起课法

> 1、想预测什么事，心念一动，立刻取数，取数可以是心中所想，也可以是看到的比如车牌号、门牌号、电话号码、时间等，要第一反应想到或看到的数。比如想问朋友在不在家，心念一动，恰巧看到手机屏幕上显示的时间是14：36分，就取1436进行测算；    <br/><br/>2、把四个数进行相加，1+4+3+6=14，然后根据你取数的位数再做减法，4位数就减去3，3位数减去2，个位数不减，本例中因为1436是4位数，故要减去3，即14-3=11；   <br/><br/>  3、把刚得到的数除以6，余数对应下边的解释（能除尽则余数是6，例如得到的数是18，则余数是6），本例11÷6→余数得5是小吉。 


看起来字挺多的，但其实很简便的逻辑。

1. 想算某件事件时，取一个你突然想到或者看到的数字，看讲解说是必须要第一反应得到的数字。

2. 比如看手机时间， 得到数字 1436。

3. 把得到的几个数字相加，减去数字的位数 - 1 ，比如1436有四位，那么数字的和减三。

4. 得出的结果除以6，最后就是结果啦。

## 代码实现

```javascript
const valueObject = [
    {
        title: '大吉',
        desc: '...'
    },
    ....
]

//  valueList 第一反应得到的活数 比如1436
const calcResult = (valueList) => {
        // 获取活数的位数 - 1  后续需要减掉
	const lenCount = valueList.length === 1 ? 0 : valueList.length - 1
        // 获取活数的相加之和
	const sum = valueList.reduce((sumValue, cur) => (sumValue += cur))
        // sum - lenCount 得到的最终活数结果 也对应着占卜结果
        // 如果能被6整除 那就是第6个占卜结果，不然就是除以6的余数
        // 最后结果 -1，因为要从数组里获得结果
	let result = (sum - lenCount) % 6 === 0 ? 5 : ((sum - lenCount) % 6) - 1
	state.cur = state.valueObject[result]
}
```
<img src="https://img0.baidu.com/it/u=2824080210,1714686751&fm=26&fmt=auto&gp=0.jpg"  width="200">


是不是很简单！

花了十几分钟弄出了个算命项目！算姻缘算事业算健康咯！

在线算卦！十元一位！ [点我算卦](https://kev1nzh37.github.io/ask-god/)
