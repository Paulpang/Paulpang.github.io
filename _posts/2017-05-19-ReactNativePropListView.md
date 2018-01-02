---
layout: post
title: ReactNative常用组件之ListView(一)原理
date: 2017-05-21
tag: HTML+ReactNative
---

### ListView原理

* ListView内部是通过ListViewDataSource这个对象，显示数据，因此使用ListView必须先创建ListViewDataSource对象。
* ListViewDataSource构造方法(创建对象):可选择性传入4个参数,描述怎么提取数据，怎么刷新cell
* 这些参数：都是函数，当产生对应的事件的时候，会自动执行这些函数.

```bash
构造函数可以接受下列四种参数（都是可选）：

getRowData(dataBlob, sectionID, rowID);
getSectionHeaderData(dataBlob, sectionID);
rowHasChanged(prevRowData, nextRowData);
sectionHeaderHasChanged(prevSectionData, nextSectionData);
```
* ListViewDataSource为ListView组件提供高性能的数据处理和访问。我们需要调用clone方法从原始输入数据中抽取数据来创建ListViewDataSource对象。
* 要更新datasource中的数据，请（每次都重新）调用cloneWithRows方法（如果用到了section，则对应cloneWithRowsAndSections方法）clone方法会自动提取新数据并进行逐行对比（使用rowHasChanged方法中的策略），这样ListView就知道哪些行需要重新渲染了

### ListView基本使用步骤

#### 1.创建数据源，但还没有给它传递数据
* 使用state保存数据源，因为数据源的数据改变的时候，需要刷新界面。
* ListView.DataSource:获取ListViewDataSource构造方法
* ListViewDataSource构造方法:决定ListView怎么去处理数据，需要传入一个对象，这个对象有四个可选属性，都是方法

```bash
getRowData(dataBlob, sectionID, rowID); 怎么获取行数据

getSectionHeaderData(dataBlob, sectionID); 怎么获取每一组头部数据

rowHasChanged(prevRowData, nextRowData); 决定什么情况行数据才发生改变，当行数据发生改变，就会绘制下一行cell

sectionHeaderHasChanged(prevSectionData, nextSectionData);决定什么情况头部数据才发生改变，当行数据发生改变，就会绘制下一行cell
```
<strong>注意：初始化ListViewDataSource的时候，如果不需要修改提取数据的方式，只需要实现rowHasChanged，告诉什么时候刷新下一行数据.</strong>

<strong>注意：默认ListViewDataSource有提取数据方式，可以使用默认的提取方式.</strong>

```bash
constructor(props) {
  super(props);
  var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
 }
```
#### 2.给数据源设置数据

```bash
constructor(props) {
  super(props);
  var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
  
  this.state = {
     // 给数据源设置数据,创建新的数据,不过保存了之前的行改变方法属性
    dataSource: ds.cloneWithRows(['row 1', 'row 2']),
  };
 }
```
#### 3.实现数据源方法，确定cell
* 这个方法会自动传入四个参数(rowData,sectionID,rowID,highlightRow)
* rowData:当前行数据
* sectionID:当前行所在组ID
* rowID：哪一行的角标
* highlightRow:高亮函数

```bash
render() {
        return (

            <View style={{flex:1}}>
                <ListView dataSource={this.state.ds}
                          renderRow={this._renderRow.bind(this)}
                />
            </View>
        )

    }

    // 实现数据源方法,每行cell外观
    _renderRow(rowData, sectionID, rowID, highlightRow) {
        return (
            <View>
                <Text>{rowData}</Text>
            </View>
        );
    }

```
### ListView分割线

```bash
 // 哪一组,哪一行,相邻行是否高亮
    _renderSeparator(sectionID, rowID, adjacentRowHighlighted)  {
        console.log(sectionID,rowID,adjacentRowHighlighted);
        return (
            <View style={{height:1,backgroundColor:'black'}}></View>
        )
    }
    
```
<strong>注意: 给cell设置分割线最好不要用上面的方法,因为在计算cell高度的时候需要加上分割线的高度,建议使用在View中设置View的borderWith属性以及borderBottomColor属性,这样在计算cell高度的时候就不需要加上分割线的高度了</strong>

### ListView头部视图

```bash
 _renderHeader() {
        return (
            <View>
                <Text>头部视图</Text>
            </View>
        )
    }
```
### ListView尾部视图

```bash
 _renderFooter() {
        return (
            <View>
                <Text>尾部视图</Text>
            </View>
        )
    }
```

### ListView点击cell高亮

```bash
  _renderRow(rowData, sectionID, rowID, highlightRow) {

		return (
           <TouchableOpacity onPress={()=>{
               AlertIOS.alert(rowID);
               highlightRow(sectionID,rowID)
           }}>
               <View>
                   <Text>{rowData}</Text>
               </View>
           </TouchableOpacity>

      );
  }
```
