This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify

## React设计模式

### 1. React基础
分离点关注经典概念--将模板与逻辑在一起，通过便携名为组件的小型代码块来组织应用
### 2. JSX
#### JSX中html元素和React元素的区别为是否以大写字母开头；
#### JSX支持自闭合标签，可以很好的保持代码简洁性；
#### JSX不是标准语言，需要转译为js 使用className代替class htmlFor代替for
#### 布尔值属性
`<button disabled />` 默认disabled为true 属性值设置为false需要显式声明
#### 展开属性
向子元素传递数据，不要按引用方式传递整个js对象，使用对象的基本属性类型值以方便校验（没懂）
用法:
`javascript
const foo = { id: 'bar'}
return <div />
`
转译结果
`javascript
var foo = { id: 'bar' };
return React.createElement('div', foo);
`
#### 常见模式
更倾向于使用JSX而不是createElement 
原因：JSX很像XML，对称开闭可以完美表示节点树
原则：
  1. 嵌套元素多行书写
  2. 如果子节点不是元素，而是文本或者变量，应该和父节点写在一行上
  3. 多行书写元素要用括号，因为JSX本质上会替换为函数，由于自动分号插入机制，另起一行可能导致意外结果
  例： `return <div />` \/\/ 成功
  `return 
  <div />` \/\/ 转换为 
  `return;
  React.createElement('div',null);`
  4. 需要检查多个变量判断是否渲染组件
    4.1 编写辅助函数检验JSX的条件语句
```javascript
canShowSecretData() {
  const { dataIsReady, isAdmin, userHasPermissions }  = this.props;
  return dataIsReady && (isAdmin || userHasPermissions)
}
<div>
   { this.canShowSecretData() && <SecretData /> }
</div>
```
    4.2 如果不喜欢函数，使用对象的getter方法使代码更加优雅
    ```
    get canShowSecretData() {
      const { dtaIsReady, isAdmin, userHasPermissions }  = this.props;
      return dataIsReady && (isAdmin || userHasPermissions)
    }
    <div>
      //就是少个函数执行括号
      { this.canShowSecretData && <SecretData />}
    </div>
    ```
    4.3 renderIf 和 react-only-if
    `renderIf`返回一个函数，接受JSX作为参数，条件为true时显示
    ```javascript
    const { dataIsReady, isAdmin, userHasPermissions } = this.props;
    const canShowSecretData = renderIf(
      dataIsReady && isAdmin && userHasPermissions
    )
    <div>
      {canShowSecretData(<SecreteData />)}
    </div>
    ```
    `react-only-if`
```javascript
const SecretOnlyIf = ((dataIsReady, isAdmin, userHasPermissions) => {
  return dataIsReady && (isAdmin || userHasPermissions )
})(SecrteData)
<div>
  <SecretDataOnlyIf
    dataIsReady={...}
    isAdmin={...}
    userHasPermissions={...}
  />
</div>
```












=======
# react-patterns-best-practices
>>>>>>> 875302a1267fe5d3976bd578b5066239cd10cc0e
