
# 初学教程3部分- 加入React的项目搭建

学习Webpack的过程可以用这样一句话描述：
>始于Bundle，陷于React。

说老实话，如果不是深入学习React的原因，很有时候我们是不可能有机会对Webpack这一当前最热门的打包工具有如此深入的学习，这句话一方面反映了React技术栈对Webpack的依赖，另外一方面可以测证出React的Webpack构建的确不是那么easy🙈。。

本部分下面的配置文件和npm依赖可以直接作用在react项目中，但是我更建议我们一起搭建属于自己的一个React的脚手架，这个过程会很有趣😏，会让我们对webpack有更深入、详细的了解。

## 必要

1. 你已经看过了前面两个部分，确认自己对Webpack和常用配置有一些基本的了解。
2. React项目的构建...当然需要对React的项目架构有一些了解，才能知道需要Webpack帮我们做什么。

## 目录

* [使用create-react-app快速构建]()
* [为React配置Babel]() 
	* [Webpack的配置]() 
	* [Babel的配置]()
* [Rendering a React Application]()
* [Babel-Based Optimizations for React]()
* [Using react-lite Instead of React for Production]()
* [Exposing React Performance Utilities to Browser]()
* [Optimizing Rebundling Speed During Development]()
* [Code Splitting with React]()
* [Maintaining Components]()
* [Conclusion]()

## 使用 create-react-app 快速构建

[create-react-app](https://www.npmjs.com/package/create-react-app)封装了很多构建react应用的最佳实践。你如果想快速构建和一个简单配置的小项目，它是非常好用的。  

create-react-app一个最具有吸引力的特性是`ejecting`。它会替代掉原本的项目依赖，让你得到一个完整的webpack配置。  

有个需要注意的问题，在你`eject`之后，你不能返回到基础依赖模式，你将不得不保持你设置的结果。


## 为React配置Babel

在Webpack中使用Babel的
























