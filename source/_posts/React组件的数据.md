---
title: React - 组件的数据 - Note(2)
categories: 技术
date: 2018-03-19 13:39:40
tags:
  - 笔记
  - React
  - 《深入浅出React和Redux》
---

- `React组件` 的数据分为两种，`prop` 和`state`。
- 无论prop或者state的改变，都可能引发组件的 **重新渲染**。
- `prop` 是组件的对外接口，`state` 是组件的内部状态。

#### React 的prop
- `prop`( property 的简写) 是从外部传递给组件的数据。
- 一个React 组件通过定义自己能够接受的`prop`就定义了自己得对外公共接口。
- 外部世界就是通过`prop`来和组件对话的。

##### 1.给 prop 赋值

```
<SampleButton
  id="sample" borderWidth={2} onClick={onButtonClick}
  style={{color: "red"}}
/>
```

<!--more-->

- 上面是一个名为 SampleButton 的组件实例，使用了名字分别为`id`、`borderWidth`、`onClick`和`style`的`prop`。
- 看起来，`prop`很像是 HTML 元素的属性，不过：
  - HTML 元素的属性的值都是字符串类型。
  - 而 React 组件的 prop所支持的类型则非常丰富，除了字符串，可以是任何一种 JavaScript 支持的数据类型。
  - borderWidth —— 数字类型
  - onClick —— 函数类型
  - style —— 是一个包含 color 字段的对象
- **当 `prop`的类型不是字符串类型时，在`JSX`中必须用花括号`{}`把`prop`值包住。**
- `style`的值有两层花括号，外层的代表`JSX`的语法，内层的花括号则代表这是一个对象常量。
- React 要求 `render` 函数只能返回一个元素。

##### 2.读取 prop 值
- 组件内部首先通过构造函数接收传入的`prop`。
- 如果一个组件要定义自己的构造函数，一定要记得在构造函数的第一行通过`super(props)`调用父类也就是`React.Component`的构造函数。
  - 如果没有调用`super(props)`，那么组件实例被构造之后，类实例的成员函数就无法通过`this.props`访问到父组件传递过来的`props`。
  - 很明显，给`this.props`赋值是`React.Component`构造函数的工作之一。

##### 3.`propTypes`检查
- React通过`propTypes`来让组件声明自己的接口规范。
  - 这个组件支持哪些`prop`。
  - 每个`prop`应该是什么样的格式。

```
Counter.propTypes = {
  caption: PropTypes.string.isRequired,
  initValue: PropTypes.number
};
```

- `caption` 必须为`string`类型，且是必须要指定的。
- `initValue`必须是`number`类型，如果没有也没关系。
- 如果不符合规范，则会在控制台`Console`里报`Warning`，但组件仍旧可以工作。
- `propTypes`虽然能在开发阶段发现代码中的问题，但放在产品环境中就不大合适了。
  - 最好的方式是，开发者在代码中定义`propTypes`，在开发时避免错误。
  - 但在发布产品时，用一种自动的方式将`propTypes`去掉，这样部署到产品环境的代码会更优。
  - 现有的`babel-react-optimize`就有这个功能，但应确保只在发布产品代码是使用它。


#### React 的state
- `state` 代表组件的内部状态。

##### 1. 初始化`state`
- 通常在构造函数结尾处初始化 `state`

```
constructor (props) {
  ...

  this.state = {
    count: props.initValue || 0
  }
}
```

- 因为`initValue`是一个可选的`props`，要考虑到父组件没有指定其值的情况。如果没有的话就使用默认值`0`。
  - 不过，让这样的逻辑充斥在构造函数中并不是一件美观的事情，而且容易有遗漏。
  - 我们可以使用React的`defaultProps`功能，使代码更易懂。

  ```
  Counter.defaultProps = {
    initValue: 0
  }
  ```

- 组建的`state`必须是一个`JavaScript`对象。


##### 2. 读取和更新`state`

```
onClickIncrementButton () {
  this.setState({count: this.state.count + 1})
}
```

- 值得注意的是，我们改变组件`state`的值必须要使用`this.setState`函数，而不能直接去修改`this.state`。
  - 因为，直接修改`this.state`的值，虽然事实上改变了组建的内部状态，但只是野蛮的修改了`state`，**却没有驱动组件进行重新渲染**，当然不会在页面上反应出变化。
  - 而`this.setState`函数所做的事情，首先是改变`this.state`的值，**然后驱动组件经历更新过程，重新渲染**。


#### prop和state的对比
- `prop`用于定义外部接口；`state`用于记录内部状态。
- `prop`的赋值在外部世界使用组件时；`state`的赋值在组件内部。
- 组件不应该改变`prop`的值；而`state`存在的目的就是让组件来改变。


- 通过`this.setState`函数修改state就是改变了组件的状态。
- 但是，组件是绝不应该去修改传入的`props`值。
