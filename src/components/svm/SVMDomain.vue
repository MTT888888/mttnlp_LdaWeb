<template>
  <div>

   <div align="center">
     <div style="width: 750px;height: 400px;background-color: #AED6F1;">
       <ul style="list-style: none">
       <li>领域：{{wh1data}}</li>
     </ul></div>
   </div>
  </div>

</template>

<script>
  import axios from 'axios';
    export default {
        name: "SVMDomain",
      data(){
          return{
            wh1data:""
          }
      },
      created:function(){
        this.wh1()
      },
      methods:
        {
          wh1: function () {
            var that = this;
            let text = document.getElementById("txt").value;
            let pa = 'http://202.196.37.144:15000/domainAnalysis?content=' + text
            const path = pa
            axios.get(path).then(function (response) {
              that.wh1data = response.data;
            }).catch(function (error) {
              alert('Error' + error)
            })
          }

        }
    }
</script>

<style scoped>

</style>
