---
title: 使用ReactNative开发狗狗说应用流程
date: 2016-12-03 10:58:58
categories: React Native
tags: 
    - React
    - React Native
    - NodeJS
    - Node
---

# 效果图

# 开发流程

## 主界面Tab切换

1.先完成主界面的三个tab切换，我们这里使用TabBarIOS

[来到官方的TabBarIOS文档](http://facebook.github.io/react-native/releases/0.22/docs/tabbarios.html#content)直接将实例代码的拷贝到项目

```javascript
var base64Icon = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEsAAABLCAQAAACSR7JhAAADtUlEQVR4Ac3YA2Bj6QLH0XPT1Fzbtm29tW3btm3bfLZtv7e2ObZnms7d8Uw098tuetPzrxv8wiISrtVudrG2JXQZ4VOv+qUfmqCGGl1mqLhoA52oZlb0mrjsnhKpgeUNEs91Z0pd1kvihA3ULGVHiQO2narKSHKkEMulm9VgUyE60s1aWoMQUbpZOWE+kaqs4eLEjdIlZTcFZB0ndc1+lhB1lZrIuk5P2aib1NBpZaL+JaOGIt0ls47SKzLC7CqrlGF6RZ09HGoNy1lYl2aRSWL5GuzqWU1KafRdoRp0iOQEiDzgZPnG6DbldcomadViflnl/cL93tOoVbsOLVM2jylvdWjXolWX1hmfZbGR/wjypDjFLSZIRov09BgYmtUqPQPlQrPapecLgTIy0jMgPKtTeob2zWtrGH3xvjUkPCtNg/tm1rjwrMa+mdUkPd3hWbH0jArPGiU9ufCsNNWFZ40wpwn+62/66R2RUtoso1OB34tnLOcy7YB1fUdc9e0q3yru8PGM773vXsuZ5YIZX+5xmHwHGVvlrGPN6ZSiP1smOsMMde40wKv2VmwPPVXNut4sVpUreZiLBHi0qln/VQeI/LTMYXpsJtFiclUN+5HVZazim+Ky+7sAvxWnvjXrJFneVtLWLyPJu9K3cXLWeOlbMTlrIelbMDlrLenrjEQOtIF+fuI9xRp9ZBFp6+b6WT8RrxEpdK64BuvHgDk+vUy+b5hYk6zfyfs051gRoNO1usU12WWRWL73/MMEy9pMi9qIrR4ZpV16Rrvduxazmy1FSvuFXRkqTnE7m2kdb5U8xGjLw/spRr1uTov4uOgQE+0N/DvFrG/Jt7i/FzwxbA9kDanhf2w+t4V97G8lrT7wc08aA2QNUkuTfW/KimT01wdlfK4yEw030VfT0RtZbzjeMprNq8m8tnSTASrTLti64oBNdpmMQm0eEwvfPwRbUBywG5TzjPCsdwk3IeAXjQblLCoXnDVeoAz6SfJNk5TTzytCNZk/POtTSV40NwOFWzw86wNJRpubpXsn60NJFlHeqlYRbslqZm2jnEZ3qcSKgm0kTli3zZVS7y/iivZTweYXJ26Y+RTbV1zh3hYkgyFGSTKPfRVbRqWWVReaxYeSLarYv1Qqsmh1s95S7G+eEWK0f3jYKTbV6bOwepjfhtafsvUsqrQvrGC8YhmnO9cSCk3yuY984F1vesdHYhWJ5FvASlacshUsajFt2mUM9pqzvKGcyNJW0arTKN1GGGzQlH0tXwLDgQTurS8eIQAAAABJRU5ErkJggg==';


var say = React.createClass( {
  statics: {
    title: '<TabBarIOS>',
    description: 'Tab-based navigation.',
  },

  displayName: 'TabBarExample',

  getInitialState: function() {
    return {
      selectedTab: 'redTab',
      notifCount: 0,
      presses: 0,
    };
  },

  _renderContent: function(color: string, pageText: string, num?: number) {
    return (
      <View style={[styles.tabContent, {backgroundColor: color}]}>
        <Text style={styles.tabText}>{pageText}</Text>
        <Text style={styles.tabText}>{num} re-renders of the {pageText}</Text>
      </View>
    );
  },

  render: function() {
    return (
      <TabBarIOS
        tintColor="#ee735c">
        <TabBarIOS.Item
          title="视频"
          icon={{uri: base64Icon, scale: 3}}
          selected={this.state.selectedTab === 'blueTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'blueTab',
            });
          }}>
          {this._renderContent('#414A8C', 'Blue Tab')}
        </TabBarIOS.Item>
        <TabBarIOS.Item
          systemIcon="history"
          badge={this.state.notifCount > 0 ? this.state.notifCount : undefined}
          selected={this.state.selectedTab === 'redTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'redTab',
              notifCount: this.state.notifCount + 1,
            });
          }}>
          {this._renderContent('#783E33', 'Red Tab', this.state.notifCount)}
        </TabBarIOS.Item>
        <TabBarIOS.Item
          icon={require('./flux.png')}
          title="More"
          selected={this.state.selectedTab === 'greenTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'greenTab',
              presses: this.state.presses + 1
            });
          }}>
          {this._renderContent('#21551C', 'Green Tab', this.state.presses)}
        </TabBarIOS.Item>
      </TabBarIOS>
    );
  }
})
```

同时在项目根目录添加一个flux.png图片，因为上面的代码引用到了，添加他只是为了能够将项目跑起来，后面会替换掉他，现在运行就能看的效果了。

## 替换Tab图标

我们这里使用一个react-native-vector-icons库，它自带了很多的图标，安装

```javascript
npm i react-native-vector-icons@2.0.2  --save
```

直接安装完还是不能直接使用的，作用就是将一些库连接到工程，包括字体和图标。这里使用rnpm

```javascript
npm i rnpm@1.7.0 -g

//连接
rnpm link react-native-vector-icons
```

现在就可以来到http://ionicons.com选择喜欢的图标了，选择后单击图标就可以得到名称。然后在代码中引入

```javascript
var Icon = require('react-native-vector-icons/Ionicons')

//将自带的tab替换为Icon.TabBarItem，他是react-native-vector-icons提供的，能更好的配合这个图标
<Icon.TabBarItem
  title="Blue Tab"
  iconName='ios-videocam-outline'
  selectedIconName='ios-videocam'
  selected={this.state.selectedTab === 'blueTab'}
  onPress={() => {
    this.setState({
      selectedTab: 'blueTab',
    });
  }}>
  {this._renderContent('#414A8C', 'Blue Tab')}
</Icon.TabBarItem>
```

特别注意icon变成了iconName，selected变为了selectedIconName，完整的tab代码

```javascript
var say = React.createClass( {
  getInitialState: function() {
    return {
      selectedTab: 'videoTab'
    };
  },

  _renderContent: function(color: string, pageText: string, num?: number) {
    return (
      <View style={[styles.tabContent, {backgroundColor: color}]}>
        <Text style={styles.tabText}>{pageText}</Text>
        <Text style={styles.tabText}>{num} re-renders of the {pageText}</Text>
      </View>
    );
  },

  render: function() {
    return (
      <TabBarIOS
        tintColor="#ee735c">
        <Icon.TabBarItem
          title="视频"
          iconName='ios-videocam-outline'
          selectedIconName='ios-videocam'
          selected={this.state.selectedTab === 'videoTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'videoTab',
            });
          }}>
          {this._renderContent('#414A8C', 'Blue Tab')}
        </Icon.TabBarItem>
        <Icon.TabBarItem
          title="录制"
          iconName='ios-recording-outline'
          selectedIconName='ios-recording'
          selected={this.state.selectedTab === 'recordTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'recordTab'
            });
          }}>
          {this._renderContent('#783E33', 'Red Tab', this.state.notifCount)}
        </Icon.TabBarItem>
        <Icon.TabBarItem
          title="更多"
          iconName='ios-more-outline'
          selectedIconName='ios-more'
          selected={this.state.selectedTab === 'moreTab'}
          onPress={() => {
            this.setState({
              selectedTab: 'moreTab'
            });
          }}>
          {this._renderContent('#21551C', 'Green Tab', this.state.presses)}
        </Icon.TabBarItem>
      </TabBarIOS>
    );
  }
})
```

## 写tab对应的页面

接下来我们需要将内容更换为三个子组件，分别对应三个tab页面。

首先先写三个组件

```javascript
var List=React.createClass({
  render:function(){
    return (
      <View style={styles.container}>
        <Text>视频列表</Text>
      </View>
    )
  }
})

var Edit=React.createClass({
  render:function(){
    return (
      <View style={styles.container}>
        <Text>制作页面</Text>
      </View>
    )
  }
})

var Account=React.createClass({
  render:function(){
    return (
      <View style={styles.container}>
        <Text>账户页面</Text>
      </View>
    )
  }
})
```

然后在tab中分别加入三个组件

```javascript
<Icon.TabBarItem
  title="视频"
  iconName='ios-videocam-outline'
  selectedIconName='ios-videocam'
  selected={this.state.selectedTab === 'list'}
  onPress={() => {
    this.setState({
      selectedTab: 'list',
    });
  }}>
  <List/> //在这里我们替换成了上面定义的组件
</Icon.TabBarItem>
```

### 将组件拿到对应的目录下

上面的组件还是放到一个文件中的，导致的问题是，多个页面逻辑都混到一个页面了，修改和删除代码都不是很方法，所以采用的方法时将每个组件都放到相应的目录，然后在入口文件导入他。

```javascript
var React = require('react-native')
var {
  StyleSheet,
  Text,
  View,
} = React;

var Icon = require('react-native-vector-icons/Ionicons')

var List=React.createClass({
  render:function(){
    return (
      <View style={styles.container}>
        <Text>视频列表</Text>
      </View>
    )
  }
})

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
})

module.exports=List
```

在入口文件中导入

```javascript
//自定义模块
var List=require('./app/list/index')
var Edit=require('./app/edit/index')
var Account=require('./app/account/index')
```

## 创建模拟数据

我们这里使用rap和mockjs。

先去rap官网创建一个项目。http://rap.taobao.org/org/index.do，配置完生成规则后，可以使用下面地址获取规则或真实数据

http://rap.taobao.org/mockjsdata/11015/api/video?accessToken=111

http://rap.taobao.org/mockjs/11015/api/video?accessToken=111

如果是规则，则需要使用mockjs解析，官网为：http://mockjs.com/

你可以在控制台下输入Mock.mock(mock规则数据试试)

```javascript
Mock.mock({"data|10":[{"_id":"@ID","video":"http:\/\/v2.mukewang.com\/cef3e514-8203-4c67-877f-79f7763553cf\/L.mp4?auth_key=1480760293-0-0-a693983f9d989e19a2c1c19f52d1e169","thumb":"@IMG(1200x600,@color())"}],"success":true})

//会输出10条测试数据
```

我们也可以直接在该页面的控制台下输入

```javascript
var d = Mock.mock({"data|10":[{"_id":"@ID","video":"http:\/\/v2.mukewang.com\/cef3e514-8203-4c67-877f-79f7763553cf\/L.mp4?auth_key=1480760293-0-0-a693983f9d989e19a2c1c19f52d1e169","thumb":"@IMG(1200x600,@color())"}],"success":true});d.data.forEach(function(item){$("#examples").append('<h3>'+item._id+'</h3><img src="'+item.thumb+'"/>')})
```

就可以看到该页面最后又很多的图片和id数组。

## 视频页面

### 添加视频页面标题

在List下面的index.js文件中添加

```javascript
<View style={styles.container}>
	<View style={styles.header}>
    	<Text style={styles.headerTitle}>列表页面</Text>
	</View>
</View>
```

然后修改样式

```javascript
var styles = StyleSheet.create({
  container: {
    flex: 1, 
    backgroundColor: '#F5FCFF',
  },

  header:{
    paddingTop:25,
    paddingBottom:12,
    backgroundColor:'#ee735c'
  },

  headerTitle:{
    color:'white',
    fontSize:16,
    textAlign:'center',
    fontWeight:'600'
  }
})
```

### 添加视频列表

添加一个ListView，首先要导出

```javascript
<ListView
  dataSource={this.state.dataSource}
  renderRow={this.renderRow}
  enableEmptySections={true}
/>
```

在定义一个renderRow方法，用来渲染每一个条目，相当于Android中Adapter的getView

```javascript
renderRow(row){

}
```

完整代码

```javascript
var List=React.createClass({

  getInitialState: function() {
    var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
    return {
      dataSource: ds.cloneWithRows([]),
    };
  },

  renderRow(row){

  },

  render:function(){
    return (
      <View style={styles.container}>
      	<View style={styles.header}>
            <Text style={styles.headerTitle}>列表页面</Text>
      	</View>
        <ListView
          dataSource={this.state.dataSource}
          renderRow={this.renderRow}
          enableEmptySections={true}
        />
      </View>
    )
  }
})
```

我们实现了一下renderRow方法

```javascript
renderRow(row){
	return(
	  <TouchableHighlight>
	    <View style={styles.item}>
	      {/* 标题 */}
	      <Text style={styles.title}>{row.title}</Text>
	      
	      {/* 图片 */}
	      <Image
	        source={{uri:row.thumb}}
	        style={styles.thumb}
	      >
	        <Icon
	          name='ios-play'
	          size={28}
	          style={styles.play} />
	      </Image>  

	      {/* 底部按钮 */}
	      <View style={styles.itemFooterContainer}>
	        <View style={styles.handleBox}>
	          <Icon 
	            name='ios-heart-outline'
	            size={28}
	            style={styles.up}  />
	          <Text style={styles.handleText}>喜欢</Text>
	        </View>
	        <View style={styles.handleBox}>
	          <Icon 
	            name='ios-chatboxes-outline'
	            size={28}
	            style={styles.commonIcon}  />
	          <Text style={styles.handleText}>评论</Text>
	        </View>
	      </View>
	    </View>
	  </TouchableHighlight>
	)
}
```

在定义一些样式

```javascript
item:{
    width:width,
    marginBottom:10,
    backgroundColor:'#fff'
  },
  thumb:{
    width:width,
    height:width*0.56,
    resizeMode:'cover'
  },
  title:{
    padding:10,
    fontSize:18,
    color:'#333'
  },
  itemFooterContainer:{
    flexDirection:'row',
    justifyContent:'space-between',
    backgroundColor:'#eee'
  },
  handleBox:{
    padding:10,
    flexDirection:'row',
    width:width/2-0.5,
    justifyContent:'center',
    backgroundColor:'#fff'
  },
  play:{
    position:'absolute',
    bottom:14,
    right:14,
    width:46,
    height:46,
    paddingTop:9,
    paddingLeft:18,
    backgroundColor:'transparent',
    borderColor:'#fff',
    borderWidth:1,
    borderRadius:23,
    color:'#ed7b66'
  },
  handleText:{
    paddingLeft:12,
    fontSize:18,
    color:'#333'
  },
  up:{
    fontSize:22,
    color:'#333'
  },
  commonIcon:{
    fontSize:22,
    color:'#333'
  }
```

样式中我们使用了屏幕的宽度，可以通过

```javascript
//导入Dimensions

// 当前屏幕宽度
var width=Dimensions.get('window').width
```



然后初始化一些假数据，然列表能显示出来

```javascript
getInitialState: function() {
	var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
	return {
	  dataSource: ds.cloneWithRows([
	        {
	            "_id":"350000197307022063","thumb":"http://dummyimage.com/1280x720/e5488e","title":"测试内容95hw","video":"http://v2.mukewang.com/cef3e514-8203-4c67-877f-79f7763553cf/L.mp4?auth_key=1480760293-0-0-a693983f9d989e19a2c1c19f52d1e169"
	        }
	        ,
	        {
	            "_id":"330000201112047039","thumb":"http://dummyimage.com/1280x720/91d5da","title":"测试内容95hw","video":"http://v2.mukewang.com/cef3e514-8203-4c67-877f-79f7763553cf/L.mp4?auth_key=1480760293-0-0-a693983f9d989e19a2c1c19f52d1e169"
	        }
	  ]),
	};
}
```

## 获取网络数据

Fetch,WebSocket,XMLHttpRequest

官方网络文档：http://facebook.github.io/react-native/releases/0.22/docs/network.html#content

我们这里使用fetch

```javascript
componentDidMount(){
	this._fetchData()
},

_fetchData(){
	fetch('http://rap.taobao.org/mockjs/11015/api/video')
	  .then((response) => response.json())
	  .then((responseText) => {
	    console.log(responseText);
	  })
	  .catch((error) => {
	    console.warn(error);
	  });
}
```

但是现在还是获取的mock规则，我们需要借助mockjs生成真是的数据

```shell
npm i mockjs --save
```

然后将生成的规则使用Mock解析，就可以得到真是数据。

```javascript
var data=Mock.mock(response)
```

> 注意：这里有个小插曲就是要删除mock.js中的dataImage方法，我们用不到canvas，所以要删掉他。

获取完网络数据后还需要判断是否请求成功，然后将数据替换到datasource中

```javascript
_fetchData(){
fetch('http://rap.taobao.org/mockjs/11015/api/video')
  .then((response) => response.json())
  .then((response) => {
    var data=Mock.mock(response)
    console.log(data)
    if (data.success) {
      this.setState({
        dataSource:this.state.dataSource.cloneWithRows(data.data)
      })
    }
  })
  .catch((error) => {
    console.warn(error);
  });
}
```

### 重构网络模块

这样写不好是因为几乎我们每个页面都要用到网络请求，通常的情况下是将网络请求封装成一个类，所以这里我们将网络请求封装到request.js中

```javascript
'use strict'

var queryString=require('query-string')
var _=require('lodash')
var config=require('./config')

var Mock=require('mockjs')

var request={}


request.get=function (url,params) {
if (params) {
	url+='?'+queryString.stringify(params)
}
return fetch(url)
		.then((response)=>response.json())
		.then((response)=>Mock.mock(response))
}

request.post=function (url,body) {
	var options = _.extend(config.header,{
		body:JSON.stringify(body)
	})

	return fetch(url,options)
			.then((response)=>response.json())
			.then((response)=>Mock.mock(response))
}

module.exports=request
```

我暴露了get,post方法，其中config是一个配置文件，包括网络的根请求地址和一些接口地址

```javascript
'use strict'

module.exports={
	header: {
	  method: 'POST',
	  headers: {
	    'Accept': 'application/json',
	    'Content-Type': 'application/json',
	  }
	},
	api:{
		base:'http://rap.taobao.org/mockjs/11015/',
		// base:'http://rap.taobao.org/mockjsdata/11015/',
		videoList:'api/video'
	}
}
```

其中我们用到了query-string，lodash需要手动安装

```javascript
npm i query-string --save
npm i lodash --save
```

这样我们首页的请求就可以改写为

```javascript
_fetchData(){
  request.get(config.api.base+config.api.videoList,{
    accessToken:'abbbb'
  })
    .then((data) => {
      console.log(data)
      if (data.success) {
        this.setState({
          dataSource:this.state.dataSource.cloneWithRows(data.data)
        })
      }
    })
    .catch((error) => {
      console.warn(error);
    });
}
```

这样就方便快捷多了,[代码变更地址为](https://git.oschina.net/lfsoft/ReactDog/commit/dd5f859537c13fdceeaec245d077e70221ea743f)

## 上拉加载更多

我们要在listview中添加一个onEndReached方法监测是否滑到了底部

```javascript
onEndReached={this._fetchMoreData}
```

然后实现_fetchMoreData方法

```javascript
_fetchMoreData(){
	if (!this._hasMore() || this.state.isLoading) {
	  //如果没有更多数据了，或者正在加载中，直接返回
	  return
	}

	var page = cacheReuslts.nextPage

	this._fetchData(page)
}
```

当然回来的数据还是得和原来的数据追加

```javascript
_fetchData(page){
	var that = this

	this.setState({
	  isLoading:true
	})

	request.get(config.api.base+config.api.videoList,{
	  accessToken:'abbbb',
	  page:page
	})
	  .then((data) => {
	    console.log(data)
	    if (data.success) {

	      var items = cacheReuslts.items.slice()

	      items=items.concat(data.data)

	      cacheReuslts.items=items
	      cacheReuslts.total=data.total

	      console.log(cacheReuslts.items.length)

	      //这里是为了有显示loading
	      setTimeout(function () {
	        that.setState({
	          isLoading:false,
	          dataSource:that.state.dataSource.cloneWithRows(cacheReuslts.items)
	        })
	      },2000)

	      
	    }
	  })
	  .catch((error) => {
	    this.setState({
	        isLoading:false
	      })
	    console.warn(error);
	  });
}
```

## 下拉刷新

使用refreshControl

```javascript
refreshControl={
	<RefreshControl
	  refreshing={this.state.isRefreshing}
	  onRefresh={this._onRefresh}
	  tintColor="#ff6600"
	  title="拼命加载中..."
	  colors={['#ff0000', '#00ff00', '#0000ff']}
	  progressBackgroundColor="#ffff00" />
}
```

然后实现_onRefresh方法

```javascript
_onRefresh(){
	if (this.state.isRefreshing) {
	  return
	}

	this._fetchData(0)
}
```

同时还得在fetchData方法里面通过判断page是否等于0来更改是刷新还是加载更多。

## 列表页点赞

这个功能分两部分，第一部分是在View中根据是否点赞显示不同的图标

```javascript
<View style={styles.handleBox}>
  <Icon 
    name={this.state.up ? 'ios-heart' : 'ios-heart-outline'}
    size={28}
    onPress={this._up}
    style={[styles.up ,this.state.up ? null : styles.down ]}  />
  <Text style={styles.handleText} onPress={this._up}>喜欢</Text>
</View>
```

第二部分是当点击了按钮，发送点赞请求

```javascript
_up(){
	var that=this

	var up = !this.state.up
	var row=this.state.row
	var url=config.api.base+config.api.up

	var body={
	  id:row._id,
	  up:up,
	  accessToken:'ab'
	}

	console.log('up')

	request.post(url,body)
	.then(function (data) {
	  if (data && data.success) {
	    that.setState({
	      up:up
	    })
	  } else{
	    AlertIOS.alert('点赞失败，请稍后重试')
	  }
	})
	.catch(function (err) {
	  console.log(err)
	  AlertIOS.alert('点赞失败，请稍后重试')
	})
}
```

请求回来了我们还得判断是否响应成功，然后改变状态，让界面刷新

## 添加进入视频详情页面

在这之前我们先要使用导航器包装

```javascript
<Navigator
	initialRoute={{
	  name:'list',
	  component:List
	}}
	configureScene={(route)=>{
	  return Navigator.SceneConfigs.FloatFromRight
	}}
	renderScene={(route,navigator)=>{
	  var Component=route.component
	  return <Component {...route.params} navigator={navigator} />
	}} />
```

这样我们就可以在List组件里面通过navigator属性拿到外面的Navigator实例，从而进入一个页面。

然后在TouchableHighlight控件上添加一个onPress方法

```javascript
_loadDetailPage(row){
	this.props.navigator.push({
	  name:'detail',
	  component:Detail
	})
}
```

这样我们就能跳转到详情页面了，现在需要实现返回到列表

```javascript
_back(){
	this.props.navigator.pop()
}
```

还要将外面的id传入详情页，我们就可以拿着id去请求详情页数据了

```javascript
_loadDetailPage(row){
	this.props.navigator.push({
	  name:'detail',
	  component:Detail,
	  params:{
	    _id:row._id
	  }
	})
}
```

然后在详情界面就可以拿到这个id

```javascript
render:function(){
	var _id = this.props._id

	return (
	  <View style={styles.container}>
	    <Text onPress={this._back}>详情页面{_id}</Text>
	  </View>
	)
}
```

那这个params是怎么传递过来了的呢，起始就是在我们包装List的时候的使用了

```javascript
<Component {...route.params} navigator={navigator} />
```

…的作用就是讲params中的所有属性展开依次传递给Component，所有我们在组件内部就能通过props拿到

## 详情页播放视频

这里使用一个第三方库

```javascript
npm i react-native-video --save

//安装完后还需要链接，我这里链接又报错，所以只能手动链接
rnpm link react-native-video
```

链接完成后，在详情界面写上Video组件

```javascript
<Video
    style={styles.video}
    ref='videoPlayer'
    source={{uri:data.video}}
    style={styles.video}
    volume={3}
    paused={false}
    rate={this.state.rate}
    muted={this.state.muted}
    resizeMode={this.state.resizeMode}
    repeat={this.state.repeat}

    onLoadStart={this._onLoadStart}
    onLoad={this._onLoad}
    onProgress={this._onProgress}
    onEnd={this._onEnd}
    onError={this._onError} />
```

## 播放和暂停

只需要控制Video组件的paused属性就行了

## 添加返回和标题栏

```javascript
<View style={styles.header}>
  <TouchableOpacity style={styles.backBox} onPress={this._pop}>
    <Icon name='ios-arrow-back' style={styles.backIcon} />
    <Text style={styles.backText} >返回</Text>
  </TouchableOpacity>
  <Text style={styles.headerTitle} numberOflines={1}>
    视频详情页
  </Text>
</View>
```

对应的样式

```javascript
header:{
    flexDirection:'row',
    justifyContent:'center',
    alignItems:'center',
    width:width,
    height:64,
    paddingTop:20,
    paddingLeft:10,
    paddingRight:10,
    borderBottomWidth:1,
    borderColor:'rgba(0,0,0,0.1)',
    backgroundColor:'#fff'
  },
  backBox:{
    position:'absolute',
    left:12,
    top:32,
    width:50,
    flexDirection:'row',
    alignItems:'center'
  },
  headerTitle:{
    width:width-120,
    textAlign:'center'
  },
  backIcon:{
    color:'#999'
  },
  backText:{
    color:'#999'
  }
```

```javascript
_pop(){
	this.props.navigator.pop()
}
```

## 视频制作者信息

```javascript
<View style={styles.infoBox} >
	<Image style={styles.avatar} source={{uri:data.author.avatar}} />
	<View style={styles.descBox}>
	  <Text style={styles.nickname} > {data.author.nickname} </Text>
	  <Text style={styles.title} > {data.title} </Text>
	</View>
</View>
```

样式

```javascript
infoBox:{
    width:width,
    flexDirection:'row',
    justifyContent:'center',
    marginTop:20
  },
  avatar:{
    width:60,
    height:60,
    marginRight:10,
    marginLeft:10,
    borderRadius:30
  },
  descBox:{
    flex:1
  },
  nickname:{
    fontSize:18
  },
  title:{
    marginTop:8,
    fontSize:16,
    color:'#666'
  }
```

## 显示视频信息

```javascript
<View style={styles.infoBox} >
	<Image style={styles.avatar} source={{uri:data.author.avatar}} />
	<View style={styles.descBox}>
	  <Text style={styles.nickname} > {data.author.nickname} </Text>
	  <Text style={styles.title} > {data.title} </Text>
	</View>
</View>
```

## 显示评论内容



### 小插曲

1.像这种布局

```javascript
<View key={row._id} style={styles.replyBox} >
	<Image style={styles.replyAvatar} source={{uri:row.replyBy.avatar}} />
	<View style={styles.reply}>
	  <Text style={styles.replyNickname} > {row.replyBy.nickname} </Text>
	  <Text style={styles.replyContent} > {row.content} </Text>
	</View>
</View>
```

replyBox的样式一定要设置宽度，不然整个页面有可能一部分显示到了左边屏幕外面了

```javascript
replyBox:{
	width:width,
	flexDirection:'row',
	justifyContent:'flex-start',
	marginTop:10
}
```

2.如果将ScrollView放到了VideoBox布局里面，将导致listview无法滚动，需要将他拿到和videoBox平级的布局中

### 优化评论布局

由于我们要显示视频信息和评论内容，所以用了ScrollView嵌套ListView

```javascript
<ScrollView
      showVerticalScrollIndicator={false}
      enableEmptySections={true}
      automaticallyAdjustContentInsets={false}
      style={styles.scrollView} >

      <View style={styles.infoBox} >
        <Image style={styles.avatar} source={{uri:data.author.avatar}} />
        <View style={styles.descBox}>
          <Text style={styles.nickname} > {data.author.nickname} </Text>
          <Text style={styles.title} > {data.title} </Text>
        </View>
      </View>

      <ListView
        dataSource={this.state.dataSource}
        renderRow={this._renderRow}
        onEndReached={this._fetchMoreData}
        renderFooter={this._renderFooter}
        onEndReachedThreshold={20}
        showVerticalScrollIndicator={false}
        enableEmptySections={true}
        automaticallyAdjustContentInsets={false}
        refreshControl={
          <RefreshControl
            refreshing={this.state.isRefreshing}
            onRefresh={this._onRefresh}
            tintColor="#ff6600"
            title="拼命加载中..."
            colors={['#ff0000', '#00ff00', '#0000ff']}
            progressBackgroundColor="#ffff00" />
        }
      />
</ScrollView>
```

显示需要去除ScrollView，这里使用renderHeader={this._renderHeader}，用法和renderFooter差不多,先返回布局

```javascript
_renderHeader(){
	var data=this.state.data

	return(
	  <View style={styles.infoBox} >
	    <Image style={styles.avatar} source={{uri:data.author.avatar}} />
	    <View style={styles.descBox}>
	      <Text style={styles.nickname} > {data.author.nickname} </Text>
	      <Text style={styles.title} > {data.title} </Text>
	    </View>
	  </View>
	)
}
```

然后删除scrollview相关的代码

```javascript
<ListView
	dataSource={this.state.dataSource}
	renderRow={this._renderRow}
	onEndReached={this._fetchMoreData}
	renderHeader={this._renderHeader}
	renderFooter={this._renderFooter}
	onEndReachedThreshold={20}
	showVerticalScrollIndicator={false}
	enableEmptySections={true}
	automaticallyAdjustContentInsets={false}
	refreshControl={
	  <RefreshControl
	    refreshing={this.state.isRefreshing}
	    onRefresh={this._onRefresh}
	    tintColor="#ff6600"
	    title="拼命加载中..."
	    colors={['#ff0000', '#00ff00', '#0000ff']}
	    progressBackgroundColor="#ffff00" />
	}
/>
```

## 添加评论

我们在视频页面添加了一个引导用户评论的输入框，但这个框起始只是一个点击层而已，目的是用户点击弹出一个浮层，在浮层里面评论

```javascript
_renderHeader(){
  var data=this.state.data

    return(
      <View state={styles.listHeader}>
        <View style={styles.infoBox} >
          <Image style={styles.avatar} source={{uri:data.author.avatar}} />
          <View style={styles.descBox}>
            <Text style={styles.nickname} > {data.author.nickname} </Text>
            <Text style={styles.title} > {data.title} </Text>
          </View>
        </View>

        <View style={styles.commentBox}>
          <View style={styles.comment}>
            <TextInput
              placeholder='敢不敢评论一个呀'
              style={styles.content}
              multiline={true}
              onFocus={this._onFocus} />
          </View>
        </View>

        <View style={styles.commentArea}>
          <Text style={styles.commentTitle}>热门评论</Text>
        </View>
      </View>
      
    )
}
```

### 提交组件

```javascript
npm i react-native-button --save
```

不需要链接,先导入

```javascript
//这种导入方式报错
//var Button=require('react-native-button')
import Button from 'react-native-button';
```

添加组件到布局

```javascript
<Button style={styles.submit} onPress={this._submit} >评论</Button>
```

添加一个_submit方法，在这里处理评论逻辑

```javascript
_submit(){
    var that = this

    if (!this.state.content) {
      return AlertIOS.alert('请输入评论内容！')
    }

    if (this.state.isSending) {
      return AlertIOS.alert('正在拼命评论中...')
    }

    //正在发送
    this.setState({
      isSending:true
    },function () {
      var body={
        accessToken:'a',
        videoId:'123',
        content:this.state.content
      }

      var url = config.api.base+config.api.comment

      request.post(url,body)
      .then(function (data) {
        if (data&&data.success) {
          var items=cacheReuslts.items.slice()

          var cotnent=that.state.content
          items=[{
            content:cotnent,
            replyBy:{
              avatar:'https://dummyimage.com/640x640/b108ca',
              nickname:'你猜猜我是谁'
            }
          }].concat(items)

          cacheReuslts.items=items
          cacheReuslts.total=cacheReuslts.total+1

          that.setState({
            content:'',
            isSending:false,
            dataSource:that.state.dataSource.cloneWithRows(cacheReuslts.items)
          })

          that._setModalVisible(false)

        }
      })
      .catch((err)=>{
        console.log(err)
        that.setState({
          isSending:false
        })

        that._setModalVisible(false)

        AlertIOS.alert('留言失败，稍后重试！')

      })
    })
  }
```

## 验证码倒计时

```javascript
npm i react-native-sk-countdown --save
```





# 屏幕单位

1英寸(inch)=2.54厘米(cm)

首先我们看iphone6

## 英寸

![](http://7qnc6h.com1.z0.glb.clouddn.com/%E5%AF%B9%E8%A7%92%E7%BA%BF.png)

## 点

![](http://7qnc6h.com1.z0.glb.clouddn.com/%E7%82%B9.png)

## 像素

![](http://7qnc6h.com1.z0.glb.clouddn.com/%E5%83%8F%E7%B4%A0.png)

## 缩放比ppi

![](http://7qnc6h.com1.z0.glb.clouddn.com/ppi.png)

## 总结

![](http://7qnc6h.com1.z0.glb.clouddn.com/iphone6-screen.png)

## iphone屏幕尺寸分布

 ![](http://7qnc6h.com1.z0.glb.clouddn.com/iphone-screen.png)

## 箭头函数

这里的箭头函数相当于java中的函数式编程

```javascript
var numberArray=[1,2,3]

// var newNumberArray=numberArray.map(function(item){
//   return item+1
// })

//等效于
var newNumberArray = numberArray.map(item=>item+1)

console.log(newNumberArray)
```

# 常见错误

## RCTSRWebSocket.m在xcode8.1下报错

http://www.jianshu.com/p/175e820a1c51

## CodeSign error: code signing is required for product type 'Unit Test Bundle' in SDK 'iOS 8.1'

http://blog.csdn.net/skymingst/article/details/42489097