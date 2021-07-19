《React 官方文档》
React 认为渲染逻辑本质上与其它 UI 逻辑内在耦合，比如，在 UI 中需要绑定处理事件、在某些时刻状态发生改变时需要通知到 UI，以及需要在 UI 中展示准备好的数据。

React 并没有采用将标记与逻辑进行分离到不同文件这种认为地分离方式，而是通过将二者共同存放在称之为“组件”的松散耦合单元之中，来实现关注点分离。

#### JSX 防止注入攻击
你可以安全地在 JSX 当中插入用户输入的内容：
```JSX
const title = response.potentiallyMaliciousInput;
// 直接使用是安全的：
const element = <h1>{title}</h1>;
React DOM
```
在渲染所有输入内容之前，默认会进行转义。它可以确保你的应用中，永远不会注入那些并非自己明确编写的内容。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS

JSX 表示对象
Babel 会把 JSX 转译成一个名为 React.createElement() 函数调用。

以下两种示例代码完全等效：

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```javascript
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
React.createElement()
```
《深入浅出 React 和 Redux》
p7：只要熟悉 HTML，学习 JSX 完全不成问题，但是，我们一定要明白两者的不同之处。

首先，在 JSX 中使用的“元素”不局限于 HTML 中的元素，可以是任何一个 React 组件，在 App 扣中可以看到，我们创建的 ClickCounter 组件被直接应用在 JSX 中，使用方法和其他元素一样，这点是传统的 HTML 做不到的

React 判断个元素是 HTML 元素还是 React 组件的原则就是看第一个字母是否大写，如果在 JSX 中我们不用 ClickCounter 而是用 clickCounter ，那就得不到我们想要的结果

其次，在 JSX 中可以通过 onClick 这样的方式给一个元素添加一个事件处理函数，当然，在 HTML 中也可以用 onclick （注意和 onClick 拼写有区别），但在 HTML 中直接书写 onclick 直就是为人垢病的写法，网页应用开发界一直倡导的是用 jQuery 的方法添加事件处理函数，直接写 onclick 会带来代码混乱的问题

这就带来一个问题，既然长期以来一直不倡导在 HTML 中使用 onclick ，为什在

#### 为什么 React JSX 中我们却要使用onClick 这样的方式来添加事件处理函数呢？

- onclick 添加的事件处理函数是在全局环境下执行的，这污染了全局环境，很容
易产生意料不到的后果；
- 给很多 DOM 元素添加 onclick 事件，可能会影响网页的性能，毕竟，网页需要的事件处理函数越多，性能就会越低；
- 于使用 onclick DOM 元素，如果要动态地从 DOM 树中删掉的话，需要把对应的时间处理器注销，假如忘了注销，就可能造成内存泄露，这样的 bug 很难被发现

首先， onClick 挂载的每个函数，都可以控制在组件范围内，不会污染全局空间

我们在 JSX 中看到一个组件使用了 onClick ，但并没有产生直接使用 onclick （注意 onclick 不是 onClick ）的 HTML ，而是使用了事件委托（event delegation ）的方式处理 点击事件，无论有多少个 onClick 出现，其实最后都只在 DOM 树上添加了一个事件处理 函数，挂在最顶层的 DOM 节点上。所有的点击事件都被这个事件处理函数捕获，然后 根据具体组件分配给特定函数，使用事件委托的性能当然要比为每个 onClick 都挂载一个事件处理函数要高

因为 React 控制了组件的生命周期，在 unmount 的时候自然能够清除相关的所有事 件处理函数，内存泄露也不再是一个问题。

