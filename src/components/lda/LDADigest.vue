<template>
  <div>


    <div align="center">
      <div style="width: 600px;height: 300px;background-color: #F7DC6F;">
        <ul v-for="www in getdata" style="list-style: none">
        <li>{{www.sentence}}}</li>
      </ul>
        <div style="width: 900px; style:20px;background: cornflowerblue;"></div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: "LDADigest",
    data() {
      return {
        wh1data:[],
        wh1site:[],
        getdata:[],
      }
    },
    created:function(){
      this.wh1()
    },
    methods:
      {
        hangde: function () {
          // alert(this.wh1site);
          console.log(this.wh1site);      //sa为json字符串
          let aaa=eval(this.wh1site);  //myobj为json对象数组
          this.getdata.push({"sentence":aaa[0].sentence});
        },
        wh1: function () {
          var that = this;
          let text = document.getElementById("txt").value;
          let pa = 'http://127.0.0.1:15001/lda/sentence?content=' + text
          const path = pa
          axios.get(path).then(function (response) {
            that.wh1site = response.data;
            // alert(that.whs1ite[2][0].sentence)
            that.hangde();
          }).catch(function (error) {
            alert('Error' + error)
          })
        }
      }
  }
</script>

<style scoped>

</style>
