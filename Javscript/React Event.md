# 目的
讲述下React中的事件的处理，其中牵涉到了React 的Synthetic Event,以及在React中的事件的异步响应

# 异步处理事件
```javascript
Class demo extends React.Componenet{
    constructor(props){
        super(props);
        this.handleEventAsyn = this.handleEventAsync.bind(this);

    }

    handleEventAsyn(e){
        this.setState((prevState,props) => (
            {status: 'e.target.value'}
        )
    }

    render(){
        return (
            <input type="text" onchange={this.handlEventAsyn}>
        );
    }
}
```
上面的这个例子中，通过异步（callback）的方式获取event对应的target的值，并返回设置到state中，这段程序无法正常执行，原因为React中的事件被包装为Synthetic事件，如果要获取对应的target，应该使用e.currentTarget事件，或者另一个方法如下
```javascript
  handleEventAsyn(e){
      e.persist();
        this.setState((prevState,props) => (
            {status: 'e.target.value'}
        )
    }
```
这里的e.persist说明事件不会被放入pool中，会维持html事件的原样。具体可以参见 [Synthetic Event in React](https://reactjs.org/docs/events.html)
