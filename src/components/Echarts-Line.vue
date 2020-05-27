<template>
    <div>
      <div :id="id" class="main"></div>
      <hr v-if="showFlag"/> 
    </div>
</template>
<script>
export default {
  name: 'EchartsLine',
  props: {
      options: {
        type: Object,
        default: {}
      },
      id: {
        type: String,
        default: ''
      },
      showFlag: {
        type:   Boolean,
        default: true
      }
  },
  data () {
    return {
    }
  },
  mounted(){
    this.drawLine();
  },
  methods: {
    drawLine(){
        let myChartq = this.$echarts.init(document.getElementById(this.id));
        let option = this.options
        // console.log(this.options, 'option1--------------')
        // 使用刚指定的配置项和数据显示图表。
        myChartq.setOption(option);
        
        // Echarts 根据浏览器窗口自适应
        window.onresize = function () {
            myChartq.resize()
        }
    }
  },
  watch: {
    options(options) {
        this.options = options
        this.drawLine()
    }
  },
}
</script>
<style>
.main {
	width: 100%; 
	height: 500px;
}
</style>