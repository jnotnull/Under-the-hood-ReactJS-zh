## Intro

## 简介

### Scheme, first look

### 整图，初次相识


[![](../images/intro/all-page-stack-reconciler-25-scale.jpg)](../images/intro/all-page-stack-reconciler.svg)

<em>Intro.0 All scheme (clickable)</em>

<em>Intro.0 整图 (可点击)</em>

So...have a look. Take your time. Overall it looks complex, but in fact, it describes only two processes: mount and update. I skipped unmount because it’s kind of ‘reversed mount’ and removing it simplified the scheme. Also, **this is not a 100%** match of the code, but only major pieces which describe the architecture. In total, it’s about 60% of the code, but the other 40% would bring little visual value. So again, for simplicity, I omitted it.

现在花点时间，自己看下。整体看上去很复杂，但是事实上，它只描述了两个处理器：mount和update。因为unmount是掉过来的mount，所以我忽略了，这样图看上去更加简洁。当然，这也不是和代码**100%吻合**，只是描述框架的主要片段，大概能覆盖60%的代码，其他40%就忽略了。

On first look, you probably noticed many colors on the scheme. Each logic item (shape on the scheme) is highlighted in its parent module's color. For example, ‘methodA’ will be red if it’s called from ‘moduleB’, which is red. Below is a legend for the modules in the scheme along with the path to each file.

第一样看上去，你可能会注意到，这幅图上有很多的颜色。每个逻辑的颜色是和父节点模块颜色相同的。举个例子，如果从红色的‘moduleB’中调用‘methodA’，那‘methodA’也是红色的。下面是图中模块对应的样色列表。

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-src-path.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-src-path.svg)

<em>Intro.1 Modules colors (clickable)</em>

<em>Intro.1 模块颜色 (可点击)</em>

Let’s put them into a scheme to see the **dependencies between modules**.

让我们通过一幅图来了解下**模块之前的依赖关系**

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/files-scheme.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/files-scheme.svg)

<em>Intro.2 Modules dependencies (clickable)</em>

<em>Intro.2 模块依赖关系 (可点击)</em>

As you probably know, React is built to **support many environments**. 
- Mobile (**ReactNative**)
- Browser (**ReactDOM**)
- Server Rendering
- **ReactART** (for drawing vector graphics using React)
- etc.

你可能知道，React**支持多种环境**. 
- 移动端 (**ReactNative**)
- 浏览器段 (**ReactDOM**)
- 服务端渲染
- **ReactART** (使用React画矢量图)
- 等等.

As a result, a number of files are actually bigger than it looks in the scheme above. Below is the same scheme with multi-support included.

这样，就有一些新的元素被加入进来了。下面这幅图描述了支持多环境的依赖图。

[![](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-per-platform-scheme.svg)](https://rawgit.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/7c2372e1/stack/images/intro/modules-per-platform-scheme.svg)

<em>Intro.3 Platform dependencies (clickable)</em>

<em>Intro.3 平台依赖关系 (可点击)</em>

As you can see, some items seem doubled. It shows they have a separate implementation for each platform. Let’s take something simple, like ReactEventListener. Obviously, its implementation will be different for different platforms! Technically, as you can imagine, these platform dependent modules should be somehow injected or connected to the current logic flow, and, in fact, there are many such injectors. Because their usage is part of a standard composition pattern, I chose to omit them. Again, for simplicity.

正如你所看到的，有些元素变成两个了。它描述了每个平台的不同实现。我们看个简单的，比如ReactEventListener，很显然，在不同平台，它的实现是不同的。正如你想到的，在技术上，这些平台依赖的模块应该通过某种方式注入或者链接到当前主流程中去。事实上，那还有很多这样的注入器。因为这种用法是典型的组合模式的一种。为了简单，我同样忽略了他们。

Let’s learn the logic flow for **React DOM in a regular browser**. It’s the most used one, and it completely covers all React’s architecture ideas. So, fair enough!

让我们学习下**React DOM in a regular browser**的逻辑流程。它算是最常用的一个了，他覆盖了所有的React框架思想，所以，足够了。


### Code sample

### 代码示例

What is the best way to learn the code of a framework or library? That's right, read and debug the code. Alright, we are gonna to debug **two processes**: **ReactDOM.render** and **component.setState**, which map on mount and update. Let’s check the code we can write for a start. What do we need? Probably several small components with simple renders, so it will be easier to debug.

学习一个框架或者库最好的方式是什么？对了，边读边调试代码。现在我们将调试**两个处理器**: **ReactDOM.render** 和 **component.setState**，分别对应mount和update。那我们就先写个简单的例子吧，只要有个render方法就可以了。

```javascript
class ChildCmp extends React.Component {
    render() {
        return <div> {this.props.childMessage} </div>
    }
}

class ExampleApplication extends React.Component {
    constructor(props) {
        super(props);
        this.state = {message: 'no message'};
    }

    componentWillMount() {
        //...
    }

    componentDidMount() {
        /* setTimeout(()=> {
            this.setState({ message: 'timeout state message' });
        }, 1000); */
    }

    shouldComponentUpdate(nextProps, nextState, nextContext) {
        return true;
    }

    componentDidUpdate(prevProps, prevState, prevContext) {
        //...
    }

    componentWillReceiveProps(nextProps) {
        //...
    }

    componentWillUnmount() {
        //...
    }

    onClickHandler() {
        /* this.setState({ message: 'click state message' }); */
    }

    render() {
        return <div>
            <button onClick={this.onClickHandler.bind(this)}> set state button </button>
            <ChildCmp childMessage={this.state.message} />
            And some text as well!
        </div>
    }
}

ReactDOM.render(
    <ExampleApplication hello={‘world’} />,
    document.getElementById('container'),
    function() {}
);
```

So, we are ready to start, let’s move on to the first part of the scheme. One by one part we will go through all of it.

那我们就从第一章开始吧

[To the next page: Part 0 >>](./Part-0.md)


[Home](../../README.md)