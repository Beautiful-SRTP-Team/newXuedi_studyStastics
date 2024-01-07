<template>
  <div v-for="(item, index) in leaderboard" :key="index" id="getdata">
    <v-list-item-content>
      <v-list-item-title>{{ item.name }}</v-list-item-title>
      <v-list-item-subtitle>{{ item.score }}</v-list-item-subtitle>
    </v-list-item-content>
  </div>
  <div style="width: auto;height: 250px" id="echarts1"></div>
  <div style="width: auto;height: 250px" id="echarts2"></div>
</template>

<script>
import echarts from 'echarts'
import axios from 'axios';


export default {
  data () {
    return {
      leaderboard: [
        { name: '难度1', score: 100 },
        { name: '难度2', score: 90 },
        { name: '难度3', score: 80 },
        { name: '难度4', score: 70 },
        { name: '难度5', score: 60 },
      ],
      // 折线图
      option1 : {
        title: {
          text: '题型统计折线图',
          left: 'center'
        },
        xAxis: {
          type: 'category',
          data: ['难度1', '难度2', '难度3', '难度4', '难度5']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            data: [100, 90, 80, 70, 60],
            type: 'line',
            smooth: true
          }
        ]
      },
      //饼状图
      option2 :{
        title: {
          text: '题型统计饼图',
          left: 'center'
        },
        tooltip: {
          trigger: 'item'
        },
        legend: {
          orient: 'vertical',
          left: 'left'
        },
        series: [
          {
            name: 'Access From',
            type: 'pie',
            radius: '50%',
            data: [
              { value: 100, name: '难度1' },
              { value: 90, name: '难度2' },
              { value: 80, name: '难度3' },
              { value: 70, name: '难度4' },
              { value: 60, name: '难度5' }
            ],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)'
              }
            }
          }
        ]
      },
    }
  },
  mounted () {
    this.echartsInit()
  },
  methods: {
    fetchCourses() {
      axios.get('http://127.0.0.1:5000/')
        .then(response => {
          let data = response.data;
          this.option1.xAxis.data=data.a;
          this.option1.series.data=data.b;
          echarts.init(document.getElementById('echarts1')).setOption(this.option1);
          echarts.init(document.getElementById('echarts2')).setOption(this.option2);
        })
        .catch(error => {
          console.error('Error fetching courses:', error);
        });
    },
    echartsInit () {
      // 在生命周期中挂载
      echarts.init(document.getElementById('echarts1')).setOption(this.option1);
      echarts.init(document.getElementById('echarts2')).setOption(this.option2);
    }
  }
}
</script>

<style scoped>

</style>
