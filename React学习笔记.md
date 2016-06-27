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

```javascript

import CounterStore  from './CounterStore' //当前文件夹下CounterStore.js是store所在的文件
import {Component} from 'react';
import {Container} from 'flux/utils';


class CounterContainer extends Component {
    //getStores,顾名思义,获取store
  static getStores() {
    return [CounterStore];
  }
    /*calculateState:当store变化时,this.state跟着变化。
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
 
