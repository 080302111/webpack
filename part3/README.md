
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
* [渲染一个React应用程序]()
* [React的Babel-Based优化]()
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

关于在Webpack中使用Babel的要领，这里有一些很明确的React设置。

大多数React项目依赖一种叫JSX的模版格式。它是JavaScript的超集，可以让我们混入类XML语法。很多人在用起来很感觉非常的方便。

一些React的开发者使用一个称为Flow的语言来扩展我们附上代码注释。这种技术和React结合良好，但是我们不仅仅只能使用它。TypeScript是另一个可行的替代方案，可以和JSX同时工作。

### Webpack的配置

Babel允许我们很容易地在React中使用JSX。有些人喜欢把他们用JSX书写的React组件用.jsx的后缀来命名。Webpack可以根据我们的意愿，基于我们的文件名来运行不同的语法规则。

Webpack提供了`resolve.extensions`的设置，可以让我们做这样的事情。如果你想允许引入import一个Button从`‘./Button’`，这个文件的名字叫`Button.jsx`，设置如下：

`webpack.config.js`

```

const common = {
	...
	resolve:{
		extensions:['.js','.jsx'],
	},
};

```

loader配置是线性依次匹配的，而不是仅仅匹配`/\.js$/`，我们可以通过`/\.(js|jsx)$/`来延伸匹配到`.jsx`。

> 在webpack 1 中你必须使用 extensions:['','.js','.jsx'] 来匹配扩展的文件名。在Webpack 2中这不是必需的了。

### Babel的配置

想要Babel能转译JSX，我们需要添加一个预设preset。安装它：

```
npm i babel-preset-react --save-dev

```

你同时也需要连接预设到Babel配置，下面是简单的设置实例：

#### .babelrc

```
{
	"presets":[
		[
			"es2015",{
				"modules":false
			}
		],
		"react"
	]
}
```

## 渲染一个React应用程序

为了让一个简单的React应用运行起来，你需要把它装载到一个DOM元素。`html-webpack-plugin`插件能够在这里派上用场。它可以结合`html-webpack-template`或者`html-webpack-template-pug`来获取更多的功能。你还可以提供一个自定义的模版。

你可以考虑下面的例子：

#### webpack.config.js

```
const HtmlWebpackPlugin = require('html-webpack-plugin');

const HtmlWebpackTemplate = require('html-webpack-template')；

const common = {
	...
	plugins:[
		new HtmlWebpackTemplate,
		title:'Demo app',
		appMountId:'app',//生成可以安装的app
		mobile:true,//缩放mobile页面
		inject:false,//html-webpack-template
	],
};

module.exports = function(env){
	...
}
```

现在有一个模版和一个DOM元素需要渲染，React需要传入参数，在那里渲染，渲染什么内容：

### app/index.js

```
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
	<div>Hello world</div>,
	document.getElementById('app')
);
```

我们可以这段代码内混入我们的应用程序，取决于我们的口味，我们可以用`index.jsx`的文件名代替这个文件，但是引用`index.js`可能更容易被接受。

> 查阅 Configuring Hot Module Replacement with React 来学习如何设置Webpack和Babel有关React代码的热重载配置项。

## React的Babel-Based优化

[babel-react-optmize](https://github.com/thejameskyle/babel-react-optimize) 实现了各种你想要尝试的React的优化。

[babel-plugin-transform-react-remove-prop-types](https://www.npmjs.com/package/babel-plugin-transform-react-remove-prop-types) 是有用的，如果我们想从生产环境中移除 propType相关的代码。它也是允许组件作者在设置不同环境变量下能够正常生产代码。

## Using react-lite Instead of React for Production

React is quite heavy library even though the API is quite small considering. There are light alternatives, such as Preact and react-lite. react-lite implements React's API apart from features like propTypes and server side rendering.

You lose out in debugging capabilities, but gain far smaller size. Preact implements a smaller subset of features and it's even smaller than react-lite. Interestingly [preact-compat](https://www.npmjs.com/package/preact-compat) provides support for `propTypes` and bridges the gap between vanilla React and Preact somewhat.

Using react-lite or Preact in production instead of React can save around 100 kB minified code. Depending on your application, this can be a saving worth pursuing. Fortunately integrating react-lite is simple. It takes only a few lines of configuration to pull off.

To get started, install react-lite:

`npm i react-lite --save-dev`

On the webpack side, we can use a `resolve.alias` to point our React imports to react-lite instead. Consider doing this only for your production setup!

```
resolve: {
  alias: {
    'react': 'react-lite',
    'react-dom': 'react-lite',
  },
},
```

If you try building your project now, you should notice your bundle is considerably smaller.

Similar setup works for Preact too. In that case you would point to preact-compat instead. See [preact-boilerplate](https://github.com/developit/preact-boilerplate) for the exact setup and more information.

[Inferno](https://www.npmjs.com/package/inferno) is yet another alternative. The setup is the same and you can find inferno-compat with a similar idea. I discuss these alternatives in more detail at my slide set known as [React Compatible Alternatives](https://presentations.survivejs.com/react-compatible-alternatives).

> If you stick with vanilla React, you can still optimize it for production usage. See the Setting Environment Variables chapter to see how to achieve this. The same trick works with preact-compat as well.





















