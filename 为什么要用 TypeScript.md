《TypeScript 实战》：

#### 什么是 TypeScript

p1 第二段：JavaScript 是弱类型的语言，设计得过于灵活，导致编写的代码可能存在预期之外的各类奇葩 Bug，因此在使用 JavaScript 构建大型可扩展的应用时，可能会出现代码后续难以升级和维护的情况。

p1 第四段：TS 具有静态类型检测和面向对象的特征，在编译阶段可以及时发现语法错误，同时支持分模块开发，编译后转换成原生的 JavaScript 代码，可以直接运行在各类浏览器上。

p3 第二段：TypeScript 是 JavaScript 的超集，专门为开发大规模可扩展的应用程序而设计，且可编译为原生 JavaScript 的一种静态类型语言。TypeScript 从命名上可以看出是由 Type 和 Script 组成的，其中 Type 表示是一种类型语言，可以进行静态类型检查，Script 表示是兼容 JavaScript 的脚本语言。

p3 第三段：编译语言中类型系统是提高代码性能的一个关键因素，类型系统对构建优化的编译器和进行语法正确性检查等非常有用。同时类型系统可以为集成开发环境（Integrated Development，简称 IDE）提供智能代码补全、重构和代码导航这些功能，而这背后都离不开具有类型系统的编译器。

p3 第四段：如果希望编程语言具有可维护性，在灵活和规范之间寻求合适的度非常重要。动态语言对于开发小型项目非常有用，但大型项目需要采用严格的类型检查。

P5 ：

TypeScript 与 ECMAScript 6 规范一致。

TypeScript 具有如下特点：

- TypeScript 以 JavaScript 为基础
- TypeScript 支持第三方 JavaScript 库
- TypeScript 是可移植的（一处编写，多处运行）
- TypeScript 是静态类型语言

#### 为什么要学习 TypeScript？

p5 第一段：TypeScript 语言的诞生是历史发展的必然。目前 Web 应用越来越复杂，必然导致 JavaScript 代码的快速增长。

p5 第二段：1、由于目前各主流浏览器中的 JavaScript 引擎还没有完全实现 ES6 的特征，如 JavaScript 模块导入和导出和面向对象编程中的类与接口等。2、JavaScript是一种动态语言，很难做到静态类型检查。这将导致很多 JavaScript 语法问题在编码阶段无法暴露，而只能在运行时暴露。

p5 第三段：在这种背景下，微软使用 Apache 授权协议推出开源语言 TypeScript，增加了可选类型、类和模块等特征，可编译成标准的 JavaScript 代码，并保证编译后的 JavaScript 代码兼容性。另外， TypeScript 是一门静态类型语言，本身具有静态类型检查的功能，很好地弥补了 JavaScript 在静态类型检查上的不足。

p6 第一段：因此，TypeScript 非常适合开发大规模可扩展的 JavaScript 应用程序。这也是我们学习 TypeScript 的主要原因。换句话说，学习 TypeScript 可以让开发和维护大规模可扩展的 JavaScript 应用程序以满足目前日益复杂的 Web 应用对 JavaScript 的要求。

p6 第二段：TypeScript 顺应了时代。TypeScript 带有编译期类型检查，在编写大规模应用程序的时候有明显优势，更容易进行代码重构和让别人理解代码的意图。

#### TypeScript 对比 JavaScript 有什么优势？

p6：

- 编译时检查
- 面向对象特征
- 更好的协作：TypeScript 支持分模块开发，这样可以更好的进行分工合作，最后在合并是解决命名冲突等问题，这对于团队协作来说是至关重要的。
- 更强的生产力：TypeScript 遵循 ES6 规范，可以让代码编辑器（IDE）实现代码智能提示，代码自动完成和代码重构等操作，这些功能有助于提高开发人员的效率。

#### TypeScript 给前端开发带来的好处

p7：

- 提高编码效率和代码质量
- 增加了代码的可读性和可维护性
- 胜任大规模应用开发
- 使用最先进的 JavaScript 语法