---
layout: post
title: ReactNative常用组件之ListView(二)基本用法
date: 2017-05-21
tag: ReactNative
---

```bash


var liveList = require('./live.json');

var {width,height} = Dimensions.get('window');

// 类
export default class App extends Component<{}> {


	// 1.数据处理
    constructor(props) {
        super(props)
        // 1.创建数据源 
        var ds = new ListView.DataSource({
            rowHasChanged:(r1,r2)=>r1 != r2
        })


        // 2.设置数据
        ds = ds.cloneWithRows(liveList)
        
        // 3.更新数据
        this.state = {
            ds:ds
        }

    }

	
    render() {
        return (
            <ListView dataSource={this.state.ds}
                      renderRow={this._renderRow.bind(this)}
                      style={{marginTop:20}}

            />
        );
    }

    //渲染每行的数据
    _renderRow(rowData) {

        return (

            <TouchableOpacity>
            <View style={{borderWidth:1,borderBottomColor:'red'}}>
                {/*顶部视图*/}
                <View style={{flexDirection:'row',width: width,height:50,alignItems:'center'}}>
                    {/*头像*/}
                    <Image source={{uri:rowData.creator.portrait}} style={{width:35,height:35,marginLeft:15}}></Image>
                    {/*名称地址*/}
                    <View style={{marginLeft:15,justifyContent:'space-between',height:35}}>
                        <Text >{rowData.creator.nick}</Text>
                        <Text>{rowData.city}</Text>
                    </View>
                    {/*粉丝*/}
                    <Text style={{position:'absolute',right:15,color:'red'}}>{rowData.online_users}
                        <Text style={{color:'black'}}>{"人在观看"}</Text>
                    </Text>
                </View>

                {/*底部视图*/}
                <Image source={{uri:rowData.creator.portrait}} style={{width:width,height:400}}/>

            </View>
            </TouchableOpacity>
        )

    }
}


```