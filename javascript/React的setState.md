# React的setState

Why setState executes in setTimeout will become sync？ 

```
componentDidMount(){
    setTimeout(() => {
            
            this.setState({ count: 1 }, () => {
                console.log(`banana`)
            })
            console.log(`lemen`)

            setTimeout(() => {
                console.log(`grape`)
            }, 0)

            this.setState({ count: 2 }, () => {
                console.log(`strawberry`)
            })

            console.log(`pear`)
        }, 0)
}

```

Why did lemen print behind banana?

the commented:
setState is only async batched when it is called inside a React event handler, otherwise it is sync. 


https://github.com/facebook/react/issues/11527

因为this.state不会立即刷新。如果立即将其刷新，我们将无法开始在后台渲染视图的“新版本”，而“旧版本”仍然可见并且可以交互。他们独立的状态更新会发生冲突。 
这样，它不会破坏之间内在一致性的保证props，state和refs。 确保提升状态是安全的。


整体意思就是，批量更新是有益于性能的。在react的钩子函数和普通函数是异步的，其他都是同步的。虽然那些setState不是异步更新，但是可以保证页面异步渲染，从而保证一致性。

关于props更新：
props直到重新渲染父组件，然后同步执行



react接收到新的props时，怎么重新渲染

子组件显示父组件穿过来的props有两种方式：
1. 直接使用
这种方式，父组件改变props后，子组件重新渲染，由于直接使用的props，所以我们不需要做什么就可以正常显示最新的props
```
class Child extends Component {
    render() {
        return <div>{this.props.someThings}</div>
    }
}

```

2. 转换成自己的state


每次子组件接收到新的props，都会重新渲染一次，除非你做了处理来阻止（比如使用：shouldComponentUpdate），但是你可以在这次渲染前，根据新的props更新state，更新state也会触发一次重新渲染，但react不会这么傻，所以只会渲染一次，这对应用的性能是有利的。

```
class Child extends Component {
    constructor(props) {
        super(props);
        this.state = {
            someThings: props.someThings
        };
    }
    static getDerivedStateFromProps(props, state){
        this.setState({someThings: props.someThings});
    }
    render() {
        return <div>{this.state.someThings}</div>
    }
}

```
getDerivedStateFromProps 会在调用 render 方法之前调用


