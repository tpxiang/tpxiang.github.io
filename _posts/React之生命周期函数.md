
### 1.什么是生命周期函数？
    react生命周期函数非常重要，对于不同阶段都有相应的执行操作。生命周期函数指的是在某一时刻自动调用执行的 
    函数。一个完整的生命周期主要分为四个阶段，分别是：Initalization（初始化阶段）、Mounting（挂载阶段）、
    Updation（更新阶段）、Unmounting（卸载阶段）。
    接下来通过一张图片对react生命周期函数做详细介绍。该图片来源于网络，如有侵权请联系删除。
[![QINRXj.md.png](https://user-gold-cdn.xitu.io/2019/12/17/16f11efec79e3bbd?w=680&h=323&f=png&s=148035)](https://imgchr.com/i/QINRXj)

    注：constructor在组件创建的时候会自动被执行，符合生命周期函数的定义，但是它不是react独有的，是es6
    语法中自带的函数，所以不将它归类到react生命周期函数。
### 2.初始化阶段
    在初始化阶段，会对props，state执行初始化操作，为下一个阶段做好准备。
### 3.挂载阶段
    挂载阶段：指的是组件第一次被挂载到页面的时候被执行。从上图可知，在挂载阶段会执行三个函数，
    componentWillMount()、render()、componentDidMount()。
>* componentWillMount：组件即将被挂载到页面的时候会被自动执行,在render之前被执行

>* render：第一次执行是在componentWillMount之后

>* componentDidMount：组件被挂载到页面之后被执行,在render之后被执行

    注：componentWillMount、componentDidMount是在组件第一次被挂载到页面的时候被执行，render不仅在
    挂载的时候会被执行，在组件发生更新时，也会被执行。
### 4.更新阶段
    在props、state更新时，该生命周期函数都会被执行。两者之间区别在于，props更新时，会执行
    componentWillReceiveProps方法。
>* componentWillReceiveProps: 该方法执行的前提是：1、当一个组件从父组件接收了参数。2、如果这个组件
    第一次存在于父组件中，不会执行。
    如果这个组件之前已经存在，就会执行。
    
>* shouldComponentUpdate: 组件被更新的时候执行，会返回true或者false, 生命周期函数会被执行  返回false表示组件不需要被更新，之后的
    生命周期函数不会被执行。一般情况都会返回true。
    
>* componentWillUpdate：组件被更新之前，它会自动执行，但是它的执行是在shouldComponentUpdate之后，并且只有shouldComponentUpdate返回true的时候才会执行该生命周期函数。
    
>* render：更新也会执行该方法，并且在componentWillUpdate之后被执行。只有shouldComponentUpdate返回true的时候才会执行该生命周期函数。该方法执行之后，视图层达到更新效果。

>* componentDidUpdate: 组件更新完成之后被执行  并且只有shouldComponentUpdate返回true的时候才会执行该生命周期函数。

    注：在组件更新时，render会被执行，但有些props、state的更新，组件的数据并未变化，render也会重新执行，这
    意味着react底层需要对组件生成虚拟DOM和之前的虚拟DOM作比对，从而消耗性能。为避免做无谓render操作，当
    content改变时才渲染页面，没有改变时不渲染页面，从而提高性能。
    
```
 render() {
    const content = this.props
    return (
      <div>
        {content}
      </div>
    )
  }
  //shouldComponentUpdate接收两个参数，nextProps表示接下来props会变成什么样。
  //nextState表示接下来state会变成什么样
shouldComponentUpdate(nextProps, nextState) {
    if (nextProps.content !== this.props.content) {
      return true
    } else {
      return false
    }
  }
```
### 5.卸载阶段
    在组件被销毁时，该阶段的方法会被执行。
>* componentWillUnmount: 当组件即将被页面中删除的时候，会被执行。
### 6.总结
    以上就是对react生命周期函数的理解。

