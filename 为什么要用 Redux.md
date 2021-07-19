《深入浅出 React 和 Redux》
#### MVC
p40：在 MVC 的世界里，React 相当于 V（也就是 View）的部分，只涉及页面的渲染一旦涉及应用的数据管理部分，还是交给 Model 和 Controller，不过，Flux 认为 MVC 框架存在很大的问题，它推翻了 MVC 框架，并用一个新的思维来管理数据流转。

p41：MVC 框架是业界广泛接受的一种前端应用框架类型，这种框架把应用分为 Model、View、Controller 三个部分

Facebook 的工程部门逐渐发现，对于非常巨大的代码库和庞大的组织，按照他们的原话说就是 “MVC 真的很快就变得非常复杂”。每当工程师想要添加一个新的功能时，对代码的修改很容易引入新的 bug，因为不同模块之间的依赖关系让系统变得 “脆弱而且不可预测”。对于刚刚加入团队的新手，更是举步维艰，因为不知道修改代码会造成什么样的后果。如果要保险，你会发现寸步难移；如果放手去干，有可能引发很多 bug。

Modol 和 View 之间缠绕着蜘蛛网一样复杂的依赖关系，根据箭头的方向，我们知道有的是 Model 调用了 View，有的是 View 调用了 Model，好乱。

p42：MVC 框架提出的数据流很理想，用户请求先达到 Controller，由 Controller 调用 Model 获得数据，然后把数据交给 View，但是，在实际框架实现中，总是允许 View 和 Model 可以直接通信，这样 Model 和 View 之间的关系错综复杂。

p42 第三段：非常遗憾的是，在一些官方的教学文档中，甚至是 Android 和 iOS 的教学文档中的例子中，也会出现 View 和 Model 直接通信的例子。不过这种状况逐渐在改变，因为越来越多的同行发现，在 MVC 中让 View 和 Model 直接对话就是灾难。

p42 第五段：服务器端 MVC 框架往往就是每个请求就只在 Controller-Model-View 三者之间走一圈，结果就返回给浏览器去渲染或者其他处理了，然后这个请求生命周期的 Controller-Model-View 三者之间走一圈，结果就返回给浏览器去渲染或者其他处理了，然后这个请求生命周期的 Controller-Model-View 就可以回收销毁了，这是一个严格意义的单向数据流；对于浏览器 MVC 框架，存在用户的交互处理，界面渲染出来之后，Model 和 View 依然存在于浏览器中，这时候就会诱惑开发者为了简便，让现存的 Model 和 View 直接对话。

p42 第六段：对于 MVC 框架，为了让数据流可控，Controller 应该是中心，当 View 要传递信息给 Model 时，应该调用 Controller 的方法，同样 Model 要更新 View 的时候，也应该通过 Controller 引发新的渲染。

当 Facebook 推出 Flux 时，招致了很多质疑。很多人都说，Flux 只不过是一个对数据流管理更加严格的 MVC 框架而已。这种说法不完全准确，但是一定意义上也说明了 Flux 的一个特点：更严格的数据流控制。

#### Flux 的优点
p43 一个 Flux 应用应该包含四个部分，我们先粗略了解下：
- Dispatcher：处理动作分发，维持 Store 之间的依赖关系
- Store：负责存储数据和处理数据的相关逻辑
- Action：驱动 Dispatcher 的 JavaScript 对象
- View：视图部分，负责显示用户界面

如果非要把 Flux 和 MVC 做一个结构对比，那么 Flux 的 Dispatcher 相当于 MVC 的 Controller，Flux 的 Store 相当于 MVC 的 Model，Flux 的 View 当然就对应 MVC 的 View 了，至于多出来的这个 Action，可以理解为对应给 MVC 框架的用户请求。

在 MVC 框架中，系统能够提供什么样的服务，通过 COntroller 暴露函数来实现。每增加一个功能，Controller 往往就要增加一个函数；在 Flux 的世界里。新增加功能并不需要 Dispatcher 增加新的函数，实际上，Dispatcher 自始至终只需要暴露一个函数 Dispatch，当需要增加新的功能时，要做的是增加一种新的 Action 类型，Dispatcher 的对外接口并不用改变。

当需要扩充应用所能处理的 “请求” 时，MVC 方法就需要增加新的 Controller，而对于 Flux 则只是增加新的 Action。

#### Flux 的不足
1、Store 之间的依赖关系
2、难以进行服务端渲染
3、Store 混杂了逻辑和状态

#### Redux

p56 Redux 的基本原则：
- 唯一数据源
- 保持状态只读
- 数据状态改变只能通过纯函数完成

唯一数据源指的是应用的状态数据应该只存储在唯一的一个 Store 上。
（因为 Flux 可以有多个 Store，容易造成数据冗余，而且依赖关系会增加复杂性，Redux 对这个问题的解决办法就是，整个应用只保持一个 Store，所有组件的数据源就是这个 Store 上的状态）

p57：保持状态只读，就是说不能直接去修改状态，要修改 Store 的状态，必须要通过派发一个 action 对象完成，这一点，和 Flux 的要求并没有什么区别。

#### 数据状态只能通过纯函数完成
这里所说的纯函数就是 Reducer，Redux 这个名字的前三个字母 Red 代表的就是 Reducer。按照作者 Dan Abramov 的说法，Redux 名字的含义是 Reducer + Flux。

就以 JavaScript 为例，数组类型就有 reduce 。里面的回调函数接收两个参数，第一个参数是上一次规约的结果，第二个参数是这一次规约的元素，函数体是返回两者之和，所以这个规约的结果就是所以元素之和。

在 Redux 中，每个 reducer 的函数签名如下所示：
reducer(state, action)

第一个参数 state 是当前的状态，第二个参数 action 是接收到的 action 对象，而 reducer 函数要做的事情，就是根据 state 和 action 的值产生一个新的对象返回，注意 reducer 必须是纯函数，也就是说函数返回的结果必须完全由参数 state 和 action 决定，而不产生任何副作用，也不能修改参数 state 和 action 对象。

p58：在 Rudex 中，一个实现同样功能的 reducer 代码：（略），可以看到 reducer 函数不光接受 action 为参数，还接受 state 为参数。也就是说，Redux 的 reducer 只负责计算状态，却不负责存储状态。

在计算机编程的世界里，完成任何一件任务，可能有一百种以上的方法，但是无节制的灵活度反而让软件难以维护，增加限制是提高软件质量的法门。


