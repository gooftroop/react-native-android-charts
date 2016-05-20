# Charts and Graphs for React Native Android
<code>react-native-android-charts</code> provides the bindings to leverage MpAndroidCharts on you React Native Android app.
Forked from [honguin163's initial implementation](https://github.com/hongyin163/react-native-chart-android)

Get started wtih MpAndroidChart:

-[**MPAndroidChart-github**](https://github.com/PhilJay/MPAndroidChart/) 

-[**MPAndroidChart-Wiki**](https://github.com/PhilJay/MPAndroidChart/wiki) 


### Installation

```
npm install react-native-android-charts --save
```

### Add it to your android project

* In `android/setting.gradle`

```gradle
include ':react-native-android-charts'
project(':react-native-android-charts').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-android-charts/android')
```

* In `android/app/build.gradle`

```gradle
...
dependencies {
  ...
  compile project(':react-native-android-charts')
}
```

* Register Module (in MainActivity.java)

```java
import cn.mandata.react_native_mpchart.MPChartPackage;  // <--- import

public class MainActivity extends Activity implements DefaultHardwareBackBtnHandler {
  ......

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    mReactRootView = new ReactRootView(this);

    mReactInstanceManager = ReactInstanceManager.builder()
      .setApplication(getApplication())
      .setBundleAssetName("index.android.bundle")
      .setJSMainModuleName("index.android")
      .addPackage(new MainReactPackage())
      .addPackage(new MPChartPackage()) // <------ add this line to yout MainActivity class
      .setUseDeveloperSupport(BuildConfig.DEBUG)
      .setInitialLifecycleState(LifecycleState.RESUMED)
      .build();

    mReactRootView.startReactApplication(mReactInstanceManager, "AndroidRNSample", null);

    setContentView(mReactRootView);
  }

  ......

}
```

## Example
```javascript
/* @flow */
'use strict';

var React = require('react-native');
var TitleBar=require('./TitleBar');
var {
  BarChart,
  CombinedChart
}=require('../index.android');
var {
  StyleSheet,
  View,
  Text
} = React;

var Component = React.createClass({
  getBarData:function (argument) {
    var data={
      xValues:['1','2','3'],
      yValues:[
        {
          data:[4.0,5.0,6.0],
          label:'test1',
          config:{
            color:'blue'
          }
        },
        {
          data:[4.0,5.0,6.0],
          label:'test2',
          config:{
            color:'red'
          }
        },
        {
          data:[4.0,5.0,6.0],
          label:'test2',
          config:{
            color:'yellow'
          }
        }
      ]
    };  
    return data;
  },
  getRandomData:function (argument) {
    var data={};
    data['xValues']=[];
    data['yValues']=[
      {
        data:[],
        label:'test1',
        config:{
          color:'blue'
        }
      }
    ];
    for (var i = 0; i < 500; i++) {
      data.xValues.push(i+'');
      data.yValues[0].data.push(Math.random()*100);
    };
    return data;
  },
  render: function() {
    return (
      <View style={styles.container}>
        <TitleBar/>
        <View style={styles.chartContainer}>
          <BarChart style={{flex:1}} data={this.getBarData()}/>
          <BarChart 
            style={{flex:1}} 
            data={this.getRandomData()}
            visibleXRange={[0,30]}
            maxVisibleValueCount={50} 
                xAxis={{drawGridLines:false,gridLineWidth:1,position:"BOTTOM"}}
                yAxisRight={{enable:false}} 
                yAxis={{startAtZero:false,drawGridLines:false,position:"INSIDE_CHART"}}
                drawGridBackground={false}
                backgroundColor={"WHITE"} 
                description={"测试"}
                legend={{enable:true,position:'ABOVE_CHART_LEFT',direction:"LEFT_TO_RIGHT"}}
            />
        </View>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container:{
    flex:1
  },
  chartContainer:{
    flex:1
  },
  chart:{
    flex:1
  }
});


module.exports = Component;

```
![alt tag](https://github.com/hongyin163/react-native-chart-android/blob/master/sample/chart1.JPG)

![alt tag](https://github.com/hongyin163/react-native-chart-android/blob/master/sample/chart2.JPG)

There are some samples in sample folder,you can download them and try to run them.
## License
MIT
