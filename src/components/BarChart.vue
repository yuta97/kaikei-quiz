<script>
import { Bar, mixins } from 'vue-chartjs'
export default {
  extends: Bar,
  name: 'BarChart',
  mixins: [mixins.reactiveProp],
  props: ['FixedAssetsA', 'CurrentAssetsA', 'CurrentLiabilitiesA', 'FixedLiabilitiesA', 'NetAssetsA', 'FixedAssetsB', 'CurrentAssetsB', 'CurrentLiabilitiesB', 'FixedLiabilitiesB', 'NetAssetsB', 'chartData'],
  data () {
    return {
      data: {
        labels: ['A', 'B'],
        datasets: [
          {
            label: 'Bar Dataset',
            data: [this.FixedAssetsA, this.CurrentAssetsA],
            backgroundColor: [
              'rgba(255, 99, 132, 0.2)',
              'rgba(74,235,21,0.2)'
            ],
            borderWidth: 1
          }
          // ,
          // {
          //   label: 'Bar Dataset',
          //   data: [10, 20],
          //   borderWidth: 1
          // },
          // {
          //   label: 'Bar Dataset',
          //   data: [0, 20],
          //   borderWidth: 1
          // }
        ]
      },
      options: {
        scales: {
          xAxes: [{
            stacked: true
          }],
          yAxes: [{
            stacked: true
          }]
        }
      }
    }
  },
  mounted () {
    console.log(this.chartData)
    this.renderChart(this.chartData, this.options)
    // console.log(this.FixedAssetsA)
    // this.renderLineChart()
  },
  methods: {
    renderLineChart: function() { this.renderChart(this.data, this.options )}
         
  
  },
  watch: {
    data: function() {
      this._chart.destroy();
      //this.renderChart(this.data, this.options);
      this.renderLineChart();
    // chartData () {
      
    //   this.$data._chart.update()
    // 
    }
  }
}
</script>
