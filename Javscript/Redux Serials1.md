# 关于Boilerplate

Redux的整个想法时来源于Flux，但是在Redu的官方文档中多次提到Boilerplate这个词，这个词的主要意思是模版，规范。按照Flux的设置，要创建一个Store,Action以及Dispatch,需要遵循很多Flux的规范，例如需要注册，需要发出消息当一个Update发生的时候

但是Redux没有这方面的限制，它只负责返回新的State,具体State的定义可以自由定义。 接受一个Action，但是具体Action的定义也是自由的，只有一个规范(Boilerplate)就是需要有Type，但是对Action处理的Reducer函数可以自由定义。

样例1
```javascript
//An light state
const LightInitial = {
    color : 'red',
    counting: false
}

//Action  
//detail description for what an action should be  https://github.com/acdlite/flux-standard-action
const TurnLight{
    Type: 'TurnGreen',
    Index: 30
}

//Reducer
function lightUpdate (state = LightInitial,action){
    switch(action.type){
        case 'TurnGreen':
            return {...state,{color:'green',counting:'true'}};
        default:
            return state;
    }
}
```

# 代码分析
1. 相对Flux，自由度更高，对应的Reducer函数只需要注意返回State
2. 注意不要更改传入的State对象
3. 缺陷在于使用了Switch ，类似If else增加了方法的不方便性（但这不属于Redux的锅）

# 新代码
```javascript
const generateLightUpdate = createReducer([],{
    ActionTypes.TurnGreen(state,action){
        return(...state,{color:'green',counting:true})
    }
})

const createReducer = (initialState,handlers) => (state = initialState,action) =>{
    return action.type && handlers[action.type] ? handlers(state,action) : state; 
}
```

1. 这是一段关于Action Type和Dispatch对应的方法，免除了IfElse

