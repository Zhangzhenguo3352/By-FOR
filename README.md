# By-FOR
这是表单
```
import React,{Component,PropTypes} from 'react';
import {Link} from 'react-router';


import Header from '../components/header.js';
import Content from '../components/content.js';

import './style/page5.css'
class Comment extends Component{
	render(){
		return(
			<div>
				<div>
					{this.props.children}
				</div>
				<div>
					- {this.props.auto}
				</div>
			</div>
		)
	}
}

class CompnentList extends Component{
	render(){
		console.log(this.props.CommentsData)
		var commentNode = this.props.CommentsData.map(function(data,index){
			return <Comment auto={data.name} key={'comment'+index}>{data.keys}</Comment>
		})
		return(
			<div>

				{commentNode}

				{/*

					<Comment auto="zhang">
					this is zhang 1
				</Comment>
				<Comment auto="zhen">
					this is zhang 2
				</Comment>
				<Comment auto="guo">
					this is zhang 3
				</Comment>
				*/}
			</div>
		)
	}
}



class ComponentForm extends Component{
	handleSubmit(e){
		e.preventDefault()			// 去除浏览器默认 刷新
		//console.log(this,e)     // this 是 ComponentForm组件， e是 事件
		const author = this.refs.author.getDOMNode().value.trim()	// 获取表单的值, 获取到 真实DOM, trim()  去除左右空格
		const body = this.refs.body.getDOMNode().value.trim()	// 获取表单的值, 获取到 真实DOM, trim()  去除左右空格
		const form = this.refs.form.getDOMNode().value.trim()	// 拿到表单的目的是 重置表单
		console.log(author,body,form)
		form.reset()
	}

	render(){
		return(
			<form className="from_page4" ref="form" onSubmit={ (e) => this.handleSubmit(e)}>
				<p><input type="text" placeholder="your name" ref="author"/></p>
				<p><input type="text" placeholder="input your txt" ref="body"/></p>
				<input type="submit" value="add Comment"/>
			</form>
		)
	}
}





// 由于是从服务器气的数据，因此下面的代码，没有必要
var CommentsData = [
					{"name":"zhang","keys":"this is zhang 1"}
					
				]
var CommentsData_2 = [
					{"name":"zhang","keys":"this is zhang 1"},
					{"name":"zhen","keys":"this is zhang 2"},
					{"name":"guo","keys":"this is zhang 3"}
				]				



class Page5 extends Component {


	// 当请求 返回成功时 改变状态机，页面重新渲染
	loderData(){
		//创建 ajax 
		var xhr = new XMLHttpRequest();
		// 初始化
		xhr.open('GET','xxx',true);
		// 注册回调监听
		console.log(__dirname+'app/module','=======')
		xhr.onreadystatechange = () => {
			if(xhr.readyState == 4){
				console.log(xhr.status,xhr.statusText)  //  状态码， 状态码描述
				console.log(xhr.responseText)  // 响应文本,服务端 返回来的数据

				//this.setState({CommentsData:xhr.responseText})
			}
		}
		xhr.send()
	}
	componentDidMount(){
		this.loderData()
	}

	constructor(props){
        super(props);
        this.state={
            conter:0,
            CommentsData:CommentsData || []     // 由于没有数据的时候，我们让它，保持空的
        };
    }
    // 为了让这个页面的 state 重新渲染，
    updata(){
    	console.log(1)
    	this.setState({
    		conter:++this.state.conter
    	})
    }
	render(){
		// setTimeout(()=>{
		// 	this.setState({
		// 		CommentsData:CommentsData_2
		// 	})
		// },2000)
		return (
			<div>
			<Header/>
	       	<Content>
	       		{/*
					<h2>登录</h2>
	       		<form>
	       			<p>用户名：<input type="text"/></p>
	       			<p>密码：<input type="text"/></p>
	       			<input type="submit"/>
	       		</form>

	       		<h2>注册</h2>
	       		<form>
	       			<p>用户名：<input type="text"/></p>
	       			<p>密码：<input type="text"/></p>
	       			<input type="submit"/>
	       		</form>
	       		*/}

	       		<div>
	       			<h2 onClick={()=>this.updata()}>Count</h2>
	       			<h3>{this.state.conter}</h3>
	       			<CompnentList CommentsData={this.state.CommentsData}/>
	       			<ComponentForm/>
	       		</div>

	       	</Content>



			</div>
		)
	}
}
export default Page5;

```