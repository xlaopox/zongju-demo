<template>
    <div class="ChartPieCircle full">
        <chart :options='options'/>
        <div class="radioBox">
            <CheckAndRadioBox :data="radio"/>
        </div>
    </div>
</template>

<script>
import CheckAndRadioBox from '../../components/tab/CheckAndRadioBox'

export default {
  name: 'ChartPieCircle',
  components: { CheckAndRadioBox },
  data () {
    return {
      radio: [{
        name: '品类',
        value: 0
      }, {
        name: '性质',
        value: 1
      }]
    }
  },
  props: {
    title: {
      type: String,
      default: ''
    },
    data: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  computed: {
    options () {
      return {
        title: {
          text: this.title
        },
        series: [
          {
            name: '访问来源',
            type: 'pie',
            radius: ['50%', '62%'],
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: true,
                fontSize: 10,
                formatter: (params) => {
                  const data = params.data
                  const percent = params.percent
                  return '{name|' + data.name + '}\n{percent|' + percent + '%}  {trend|' + data.trend + '}'
                },
                rich: {
                  name: {},
                  percent: {},
                  trend: {},
                  status: {}
                }
              },
              emphasis: {
                show: true
              }
            },
            data: this.data
          }
        ]
      }
    }
  }
}
</script>

<style scoped lang="less">
.ChartPieCircle {
    position: relative;

    .radioBox {
        position: absolute;
        height: 40px;
        width: 100px;
        background-color: #42b983;
        top: 0;
        right: 0;
    }
}
</style>
