## 1. flux-util中一般会使用到Store,Store中有时会使用到Immutable,
immutable常用的方法有
```js
var dictDataPlain  = new Immutable.Map(); //新建
set //修改
get //获取

toJSON() //map转为json,对于调试很有用


```
## 2. flux-util中calculateState的作用是什么?调用的时机是什么?
calculateState是Container中概念。
Container的作用是:当相关的store变换时,自动更新其state

> Create is used to transform a react class into a container that **updates its state when relevant stores change**. 

```react

import CounterStore  from './CounterStore' //当前文件夹下CounterStore.js是store所在的文件
import {Component} from 'react';
import {Container} from 'flux/utils';


class CounterContainer extends Component {
    //getStores,顾名思义,获取store
  static getStores() {
    return [CounterStore];
  }
    /*calcu
    lateState:当store变化时,this.state跟着变化。
    * ~~ 此处类似于,this.state.counter = CounterStore.getState()。~~
    * (其实不能写类似this.state.** = **的代码,应该是类似this.setState(counter,CounterStore.getState());)
    */
  static calculateState(prevState) {
    return {
      counter: CounterStore.getState(),
    };
  }

  render() {
    return <CounterUI counter={this.state.counter} />;
  }
}

const container = Container.create(CounterContainer);

```
 ## 3. Material-UI 中的CircularProgress如何居中?
 ```react
                 <CircularProgress
                     style={{ marginLeft: '50%', left: -20 }}
                 />
 ```
 ## 4. React如何定义一个空的Component?
 ```react
  = null;
 ```
 ## 5. JSX props should not use .bind()?
 ### Why not?
 因为每次render都会创建一个新的函数,这样会对性能有影响。[More](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)
 ### 如果实在需要bind怎么办呢?
 TODO
 ## 6.propTypes的作用什么?
 答:指定props中的接受的类型
 
 [facebook的官方说明](https://facebook.github.io/react/docs/reusable-components.html)
 
如果直接抄写
 ```javascript  
 React.createClass({
     propTypes: {
         optionalArray: React.PropTypes.array,
     }
     ****
 })
 ```
 类似的代码是会报错的。
 
**正确的方式如下:**
 
 ```javascript
 class DictPicker extends Component {
        ****
 }
 DictPicker.propTypes = {
     onChange: React.PropTypes.func.isRequired,
     label: React.PropTypes.string,
     controlState: React.PropTypes.object,
     comp: React.PropTypes.object,
     title: React.PropTypes.string,
     children: React.PropTypes.element,
     selectedValue: React.PropTypes.string
 };
 ```
 为什么官方的代码不能工作呢?
 
 答:react13以前可以使用官方的的代码;现在要使用ES7规范的写法。只是写法不同,本质相同。[More](https://github.com/yannickcr/eslint-plugin-react/issues/203)
 ## 7.Failed propType: Invalid prop `children` supplied to `DictPopup`, expected a single ReactElement. Check the render method of `YESDict`.?
 PropTypes设置不正确。
 ```react
 <DictDialog
     title={this.props.label}
     comp={comp}
     onChange={(v) => this.onChange(v)}
     style={{ left: 0, bottom: 0 }}
 >
     <Cell>
         <CellHeader>
             <label className="weui_label">{this.props.label}</label>
         </CellHeader>
         <CellBody>{state.get('displayValue')}</CellBody>
         <CellFooter />
     </Cell>
     <Divider />
 </DictDialog>
 ```
 这段代码中DictDialog Component的children包含两个subComponent:Cell和Divider。
 那么在设置DictDialog的PropTypes时候应该真么设置:
  ```react   
  DictDialog.propTypes = {
      children: React.PropTypes.array
  };
  ```
  如果DictDialog下面可能是array[Cell,Divider],也可能只有一个[Cell]呢?那么他的proptTypes应该是下面这样的:
 ```react   
 DictDialog.propTypes = {
     children: React.PropTypes.oneOfType([
         React.PropTypes.array,
         React.PropTypes.element,
     ])
 };
 ```
## 8. Required context `muiTheme` was not specified in `List`

  ```error
  warning.js?8a56:45 Warning: Failed Context Types: Required context `muiTheme` was not specified in `List`. Check the render method of `FluxContainer(DictPicker)`.
  ```
  ```
  ListItem.js?b121:399 Uncaught (in promise) TypeError: Cannot read property 'prepareStyles' of undefined(…)
  ```
  中文解释: List的parent Component没有Theme,需要自己添加Theme
  解决办法:
  ```javascript  
   import getMuiTheme from 'material-ui/styles/getMuiTheme';
   import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
   
                  <MuiThemeProvider muiTheme={getMuiTheme()}>
                      <List onTap={(event)=>this.onClick(event)} onValueChange={(v)=>this.onValueChange(v)} >
                          {
                              itemList
                          }
                      </List>
                  </MuiThemeProvider>
  ```
## 9. JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。
##10. Why code like this {{left: -20}}? 两个"{"?
第一个"{"是指里面的内容使用javascript解析,第二个"{"代表对象。
## 10.this.props.children
this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点