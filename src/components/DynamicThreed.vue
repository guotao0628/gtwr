<template>
    <div id="hello">
      <div id="dynamic"></div>
    </div>
</template>

<script>
require('../style/login.scss')
import echarts from 'echarts'
import'echarts-gl'
import linedata from '../assets/data/test.json'

export default {
  name: 'hello', 
  data () {
    return {
      myChart:null
    }
  },
  mounted(){
     this.dynamicThreeD();
  },
  beforeDestroy(){
    this.myChart.clear();
  },
  methods:{
    coltowgs:function(LONCOL, LATCOL) {
      let lat1 = 30.6666667;
      let lat2 = 31.8833333;
      let lon1 = 120.866667;
      let lon2 = 122.2;
      let accuracy = 500;
      let latStart = Math.min(lat1, lat2);
      let lonStart = Math.min(lon1, lon2);
      let deltaLon = accuracy * 360 / (2 * Math.PI * 6371004 * Math.cos((lat1 + lat2) * Math.PI / 360));
      let deltaLat = accuracy * 360 / (2 * Math.PI * 6371004);
      let HBLON = LONCOL * deltaLon + (lonStart - deltaLon / 2)
      let HBLAT = LATCOL * deltaLat + (latStart - deltaLat / 2)
      return [HBLON, HBLAT]
    },
    //绘制三维动态可视化效果
    dynamicThreeD:function(){
      let dom = document.getElementById("dynamic");
      this.myChart = echarts.init(dom);
      let app = {};
      mapboxgl.accessToken ='pk.eyJ1IjoiZ2VtbWFhYWEiLCJhIjoiY2o2a2N5dzB1MWd1ZTMzcnlqMDhkM3ZjYyJ9.0vVVkY9k7t8z0e3uqMgQnQ';
      let option = {
        baseOption: {
          timeline: {
            axisType: 'category',
            orient: 'vertical',
            autoPlay: true,
            inverse: true,
            playInterval: 500,
            left: null,
            right: 0,
            top: null,
            bottom: 50,
            width: 55,
            height: null,
            show:false,
            label: {
                normal: {
                    textStyle: {
                        color: '#fff'
                    }
                },
                emphasis: {
                    textStyle: {
                        color: '#aaa'
                    }
                }
            },
            symbol: 'circle',
            lineStyle: {
                color: '#555'
            },
            checkpointStyle: {
                color: '#bbb',
                borderColor: '#777',
                borderWidth: 2
            },
            controlStyle: {
                normal: {
                    color: '#666',
                    borderColor: '#666'
                },
                emphasis: {
                    color: '#aaa',
                    borderColor: '#aaa'
                }
            },
            data: []
          },
          visualMap: {
              show: false,
              calculable: true,
              realtime: false,
              inRange: {
                  color: ['#313695', '#4575b4', '#74add1', '#abd9e9', '#e0f3f8', '#ffffbf', '#fee090', '#fdae61', '#f46d43', '#d73027', '#a50026']
                  /*color:['#c7ffec','#83FCD8','#66ccff','#66cccc','#dcf7a1',
                  '#ffe957' ,'#ff6600','#ff0033']*/
                  /*color:['#83FCD8','#04dd98','#5af580','#d2f557','#ffe957','#ff6600','#ff0033']*/
                  /*color:[ '#6235E0','#ff7400','#FFFEA0','#ff7400']*/
              },
              outOfRange: {
                  colorAlpha: 0
              }
          },
          mapbox: {
            center: [120.5393, 31.323070],
            zoom: 9,
            minZoom:8,
            maxZoom:11,
            pitch: 45,
            bearing: -0,
            style: 'mapbox://styles/mapbox/satellite-v9',
            boxHeight: 25,
            //altitudeScale: 1,
            postEffect: {
                enable: true,
                SSAO: {
                    enable: true,
                    radius: 2,
                    intensity: 1.5
                }
            },
            shading:'color',
          },
          series: [{
              type: 'bar3D',
              shading: 'realistic',
              coordinateSystem: 'mapbox',
              barSize: 0.16,
              silent: true
          }]
        },
        options: []
      }
      for (let n = 0; n < linedata[2].length; n++) {
          option.baseOption.timeline.data.push(linedata[2][n]);
          let timedata = linedata[0][n]
          let data = []
          for (let i = 0; i < timedata.length; i += 1) {
              let loncol = linedata[0][n][i][0]
              let latcol = linedata[0][n][i][1]
              let count = linedata[0][n][i][2]
              let coor = this.coltowgs(loncol, latcol)
              data.push({
                  'value': [coor[0], coor[1], count]
              })
          }
          data.push({
              'value': [120, 30, linedata[1]]
          })
          option.options.push({

              visualMap: {
                  max: linedata[1]
              },
              series: [{
                  data: data
              }]
          });
      }
      if (option && typeof option === "object") {
          this.myChart.setOption(option, true);
      }
    }
  }
}
</script>