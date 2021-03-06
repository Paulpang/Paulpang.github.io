---
layout: post
title: ReactNative常用组件之ListView(三)分组样式
date: 2017-05-22
tag: ReactNative
---

### ListView分组原理

ListView默认支持3种数据格式,只要按照这3种格式处理数据，就会自动获取数据,从而达到分组样式
默认的提取函数可以处理下列形式的数据:

```bash
{ sectionID_1: { rowID_1: rowData1, ... }, ... }

或者：

{ sectionID_1: [ rowData1, rowData2, ... ], ... }

或者：

[ [ rowData1, rowData2, ... ], ... ]

```
<strong>注意 : 建议将数据处理成第二种样式.</strong>

### 实现ListView分组样式步骤

#### 1.创建数据源,描述什么时候需要加载下一个cell和下一个section
```bash
// 1.创建数据源
        var dataSource = new ListView.DataSource({
            rowHasChanged:(r1,r2)=>r1 !== r2,
            sectionHeaderHasChanged:(s1,s2)=>s1 !== s2
        });
```
#### 2.处理数据，让数据跟默认提前的格式一样
```bash
var sectionData = {};
        for (var i = 0;i < provinceList.length;i++){
            var province = provinceList[i];
            var cityList = province['sub'];

            var cityArr = [];
            for(var cityIndex = 0;cityIndex < cityList.length;cityIndex++) {
                var city = cityList[cityIndex];
                cityArr.push(city['name']);
            }
            sectionData[province['name']] = cityArr;
        }
```
#### 3.设置数据
* 分组使用：cloneWithRowsAndSections
* 不分组使用：cloneWithRows

```bash
this.state = {
            ds : dataSource.cloneWithRowsAndSections(sectionData)
        }
```
#### 4.渲染listView

```bash
 render() {
        return (

            <View style={{flex:1,marginTop:20}}>
                <ListView dataSource={this.state.ds}
                          renderRow={this._renderRow.bind(this)}
                          renderSectionHeader={this._renderSectionHeader.bind(this)}
                          renderSeparator={this._renderSeparator.bind(this)}
                />
            </View>
        )

    }
    _renderSeparator() {
        return (
            <View style={{height:1,backgroundColor:'#e8e8e8'}}/>
        )
    }

    _renderSectionHeader(sectionData, sectionID) {
        return (
            <View style={{backgroundColor:'rgb(247,247,247)'}}>
                <Text style={styles.sectionStyle}>{sectionID}</Text>
            </View>
        )
    }

    // 实现数据源方法,每行cell外观
    _renderRow(rowData, sectionID, rowID, highlightRow) {
        return (
            <View style={{backgroundColor:'white',height:45,justifyContent:'center'}}>
                <Text style={styles.rowStyle}>{rowData}</Text>
            </View>
        );
    }
```
