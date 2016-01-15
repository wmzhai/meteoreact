## Meteor 1.3 React Demo

具体内容参考Arunoda的[Getting Started with Meteor 1.3 and React](https://voice.kadira.io/getting-started-with-meteor-1-3-and-react-15e071e41cd1#.3eh6hnjog)。


### Meteor项目创建

```bash
meteor create —-release 1.3-modules-beta.4 myapp
cd myapp
rm -rf *
```

### 初始化NPM

通过如下指令创建一个`packages.json`文件，从而将app变成一个NPM模块，也方便从NPM获取React package来使用。

```bash
npm init -f
```

### NPM添加React
注意，我们通过npm的方式来添加，而不是使用meteor add的方式来添加，配置信息保存在`packages.json`文件里，而不是`.meteor/packages`。
这里需要避免使用meteor里面的react package，那样会有两个不同版本的react。

```bash
npm i --save react react-dom
```

### 添加UI Components
创建文件`client/app.jsx`如下

```js
import React from 'react';

// define and export our Layout component
export const Layout = ({content}) => (
    <div>
        <h1>My App</h1>
        <hr />
        <div>{content}</div>
    </div>
);

// define and export our Welcome component
export const Welcome = ({name}) => (
    <div>
        Hello, {name}.
    </div>
);
```



### Meteor添加FlowRouter和react-mounter

这里的`react-mounter`代替了原来的`react-layout`的作用。

```bash
meteor add kadira:flow-router
npm i --save react-mounter
```

### 添加router

`client/routes.jsx`

```js
import React from 'react';
import {mount} from 'react-mounter';
// load Layout and Welcome React components
import {Layout, Welcome} from './app.jsx';

FlowRouter.route("/", {
  action() {
    mount(Layout, {
        content: (<Welcome name="Meteor 1.3"/>)
    });
  }
});
```

### 运行程序

```bash
meteor
```
