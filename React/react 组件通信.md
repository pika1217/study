---
title: React 组件通信
date: 2017-8-23
tags: React
categories: React
---
## 父=>子通信
父组件可以通过props向子组件传递信息

```
//子组件
var Child = React.createClass({
    render: function(){
        return (
            <div>
                {this.props.emailSon}
            </div>
        )
    }
});
//父组件，此处通过event.target.value获取子组件的值
var Parent = React.createClass({
    render: function(){
        return (
            <div>
                <Child name="email" emailSon={this.state.email}/>
            </div>
        )
    }
});
```

## 子=>父通信
1. react中state改变了，组件才会update。父写好state和处理该state的函数，同时将函数名绑定this并且通过props属性值的形式传入子组件，子通过this.props调用父的函数，同时使用setState引起state变化。子组件要写在父组件之前。（父级可以将一个回调函数当作属性传递给子级，子级可以直接调用函数从而和父级通信。）

```
//子组件
var Child = React.createClass({
    render: function(){
        return (
            <div>
                请输入邮箱：<input onChange={this.props.handleEmailSon}/> //输入的改变会触发父组件中的handleEmail函数
            </div>
        )
    }
});
//父组件，此处通过event.target.value获取子组件的值
var Parent = React.createClass({
    getInitialState: function(){
        return {
            email: ''
        }
    },
    handleEmail: function(event){
        this.setState({email: event.target.value});
    },
    render: function(){
        return (
            <div>
                <div>用户邮箱：{this.state.email}</div>
                <Child name="email" handleEmailSon={this.handleEmail.bind(this)}/>
            </div>
        )
    }
});
React.render(
  <Parent />,
  document.getElementById('test')
);
```
2. 有时候需要随时调用父组件中的函数而不是需要事件触发才能调用，并且需要对数值进行一些处理

```
//子组件，handleVal函数处理用户输入的字符，再传给父组件的handelEmail函数
var Child = React.createClass({
    handleVal: function() {
        var val = this.refs.emailDom.value;
        val = val.replace(/[^0-9|a-z|\@|\.]/ig,"");
        this.props.handleEmail(val);  //经过处理之后再调用父方法并传值
    },
    render: function(){
        return (
            <div>
                请输入邮箱：<input ref="emailDom" onChange={this.handleVal}/>
            </div>
        )
    }
});
//父组件，通过handleEmail接受到的参数，即子组件的值
var Parent = React.createClass({
    getInitialState: function(){
        return {
            email: ''
        }
    },
    handleEmail: function(val){
        this.setState({email: val});
    },
    render: function(){
        return (
            <div>
                <div>用户邮箱：{this.state.email}</div>
                <Child name="email" handleEmail={this.handleEmail.bind(this)}/>
            </div>
        )
    }
});
React.render(
  <Parent />,
  document.getElementById('test')
);
```
3. 如果组件存在嵌套，则需要一层一层的传递

```
//孙子，将下拉选项的值传给爷爷
var Grandson = React.createClass({
    render: function(){
        return (
            <div>性别：
                <select onChange={this.props.handleSelect}>
                    <option value="男">男</option>
                    <option value="女">女</option>
                </select>
            </div>
        )
    }
});
//子，将用户输入的姓名传给爹  
//对于孙子的处理函数，父只需用props传下去即可
var Child = React.createClass({
    render: function(){
        return (
            <div>
                姓名：<input onChange={this.props.handleVal}/>
                <Grandson handleSelect={this.props.handleSelect}/>
            </div>
        )
    }
});
//父组件，准备了两个state，username和sex用来接收子孙传过来的值，对应两个函数handleVal和handleSelect
var Parent = React.createClass({
    getInitialState: function(){
        return {
            username: '',
            sex: ''
        }
    },
    handleVal: function(event){
        this.setState({username: event.target.value});
    },
    handleSelect: function(event) {
        this.setState({sex: event.target.value});
    },
    render: function(){
        return (
            <div>
                <div>用户姓名：{this.state.username}</div>
                <div>用户性别：{this.state.sex}</div>
                <Child handleVal={this.handleVal.bind(this)} handleSelect={this.handleSelect.bind(this)}/>
            </div>
        )
    }
});
React.render(
  <Parent />,
  document.getElementById('test')
);
```


