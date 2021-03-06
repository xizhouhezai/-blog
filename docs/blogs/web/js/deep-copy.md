---
title: 深拷贝和浅拷贝与引用传递
date: 2020-07-17
tags:
 -  js
categories:
 - web前端
---

## 深拷贝和浅拷贝与引用传递

虽然时常会遇到人问深拷贝和浅拷贝的问题，但实际偏业务开发中很难遇到深拷贝和浅拷贝的问题，久而久之也会注意不到深拷贝和浅拷贝在一些实际情况下造成的影响，而造成这一问题的正是引用类型数据的引用传递特性。引用类型在赋值的时候，只会把指针赋给新的变量，实际上是内存地址，不是真正的数据，所以当赋给新的变量修改引用类型数据时，旧的也会发生改变。这既有好处，也有坏处，这就是问题的所在之处。有的时候你希望原始的变量一起改变，有的时候你又不希望。但是总的来说不管哪种，都会有些问题存在。

## 遇到的问题

这是一个实际遇到的问题，我希望把一个一维数组变成二维数组，最简单的做法，如下

```js
function arrTrans (num, arr) {
  const newArr = []
  while(temp.length > 0) {
    newArr.push(temp.splice(0, num))
  }
  return newArr
}
```

如果不考虑原数组还继续使用，其实并没有什么问题，不巧的是，这正处于尴尬的处境，我希望继续使用原数组。这个问题一开始，我是没有什么意识的，所以当我在做功能时，老是数据是空的，很是懵。然后在几处打印，开始有，然后突然没有了，我还没想清楚时，觉得可能发生了什么天大的事。我反复审查代码，到了要抓破头皮的地步，本来头发不多，现在更少了。这就是突然遇上一个不常用且不太注意的知识点时，带来的疑惑。如果你使用强语言类型的语言，那么指针的问题可能时时叫你做人，可是遇到js这种过于随意的语言，有的时候会忽略很多东西，一样可以搞下去。这可能没有什么不好，自由的放纵，随心所欲，每个js程序员写起代码时，那叫一个爽字了得，但是不得不说，自由是相对的，这个相对却是绝对的，虽然拗口，仔细想想，还是有那么几分道理的。

既然提到自由这个话题，又不得不唠叨几句，js自由的放纵，可是维护起来却是自由的想放弃。一些完全不写注释和完全没有代码风格的js者们，奉劝你们一句，下班小心了 :dog: :dog: :dog: :dog:

言归正题，有时候灵光总是奇怪一闪，在左看右看奇怪的现象下，突然想起，数组是引用数据，他有个特性，就是不管你把这个数组的原始变量再赋给多少个变量，实际都是一样的。想通这一点，问题很快就解决了。其实问题不难，其难度在于经验，如果遇到的多了，一眼就能看穿，有人会说这是基础知识没掌握好，我不怎么认为，就算你的基础知识再丰富，掌握的再牢固，如果没有实战的经验，遇到一些问题也会发蒙，不知道用哪个知识点去解决，有知识，和会不会用，有时候是两码事。

## 解决问题

问题解决的办法很简单，就是在一维数组变成二维数组前对，旧数组进行深拷贝，只要在原先的基础上加上一行代码即可

```js
function arrTrans (num, arr) {
  const newArr = []
  const temp = arr.concat()
  while(temp.length > 0) {
    newArr.push(temp.splice(0, num))
  }
  return newArr
}
```

concat方法可以对一维数组进行深拷贝
