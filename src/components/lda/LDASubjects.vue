<template>
  <div>
    <ul v-for="www in getdata" style="list-style: none">
      <li>{{www.word}}{{www.weight}}</li>
    </ul>
    <div align="center">
      <div id="chart" style="width: 750px;height: 400px;background-color: #82E0AA;">


      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "LDASubjects",
    data() {
      return {
        whdata:[],
        whsite:[],
        getdata:[]
      }
    },
    created:function(){
      this.wh()
    },
    methods: {
      hangde:function(){
        let i=0
        for(;i<this.whsite[0].length&&i<7;i++){
          this.getdata.push({"word":this.whsite[0][i].word,"weight":this.whsite[0][i].weight});
        }
        // alert(this.getdata)
      },
      wh: function () {
        var that = this;
        let text=document.getElementById("txt").value;
        let pa='http://127.0.0.1:15001/lda/word?content='+text
        const path=pa
        axios.get(path).then(function (response) {
          that.whsite = response.data;
          // that.hangde();
          that.charts();
          console.log(that.whsite);
          //alert(that.whsite[0][0].word)

        }).catch(function (error) {
          alert('Error' + error)
        })
      },
      charts(){
        console.log(this.whsite);      //sa为json字符串
        let zzz=eval(this.whsite);  //myobj为json对象数组
        var chart=this.$echarts.init(document.getElementById("chart"));
        var name=[];
        var value=[];
        for(var i=0;i<zzz.length;i++){
          name[i]=zzz[i].word;
          value[i]=zzz[i].weight;
        }
        this.option = {
          color: ['#3398DB'],
          tooltip : {
            trigger: 'axis',
            axisPointer : {            // 坐标轴指示器，坐标轴触发有效
              type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
            }
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          xAxis : [
            {
              type : 'category',
              data : name,
              axisTick: {
                alignWithLabel: true
              }
            }
          ],
          yAxis : [
            {
              type : 'value'
            }
          ],
          series : [
            {
              name:'直接访问',
              type:'bar',
              barWidth: '60%',
              data:value
            }
          ]
        };
        chart.setOption(this.option)

      },
    },

  mounted(){
    // this.charts()
  }
  }
</script>

<style scoped>

</style>
