<template>
  <div id="app">
    <!-- <p>colgroup のある表</p> -->
    <table>
      <tr>
        <th></th>
        <th>A</th>
        <th>B</th>
      </tr>
      <tr>
        <td>固定資産</td>
        <td><input v-model.number="FixedAssetsA" >{{FixedAssetsA}}</td>
        <td><input v-model.number="FixedAssetsB" >{{FixedAssetsB}}</td>
      </tr>
      <tr>
        <td>流動資産</td>
        <td><input v-model.number="CurrentAssetsA" >{{CurrentAssetsA}}</td>
        <td><input v-model.number="CurrentAssetsB" >{{CurrentAssetsB}}</td>
      </tr>
      <tr>
        <td>流動負債</td>
        <td><input v-model.number="CurrentLiabilitiesA" >{{CurrentLiabilitiesA}}</td>
        <td><input v-model.number="CurrentLiabilitiesB" >{{CurrentLiabilitiesB}}</td>
      </tr>
      <tr>
        <td>固定負債：</td>
        <td><input v-model.number="FixedLiabilitiesA" >{{FixedLiabilitiesA}}</td>
        <td><input v-model.number="FixedLiabilitiesB" >{{FixedLiabilitiesB}}</td>
      </tr>
      <tr>
        <td>純資産</td>
        <td><input v-model.number="NetAssetsA" >{{NetAssetsA}}</td>
        <td><input v-model.number="NetAssetsB" >{{NetAssetsB}}</td>
      </tr>
    </table>
    <button @click="showChart()" >グラフを作る</button>
    <BarChart :chart-data="datacollection" :options="options"/>
  </div>
</template>

<script>
import BarChart from '@/components/BarChart.vue'
export default {
  name: 'App',
  components: {
    BarChart
  },
  data: () => ({
    FixedAssetsA: 50,
    CurrentAssetsA: 40,
    CurrentLiabilitiesA: 30,
    FixedLiabilitiesA: 30,
    NetAssetsA: 30,
    FixedAssetsB: 50,
    CurrentAssetsB: 40,
    CurrentLiabilitiesB: 30,
    FixedLiabilitiesB: 30,
    NetAssetsB: 30,
    datacollection: null,
    options: null
  }),
  mounted () {
    this.showChart()
  },
  methods: {
    showChart () {
      this.datacollection = {
        labels: ['A', 'A', 'B', 'B'],
        datasets: [
          {
            label: '純資産',
            data: [0, this.CurrentLiabilitiesA / (this.CurrentLiabilitiesA + this.FixedLiabilitiesA + this.NetAssetsA), 0, this.CurrentLiabilitiesB / (this.CurrentLiabilitiesB + this.FixedLiabilitiesB + this.NetAssetsB)],
            backgroundColor: [
              'rgba(255, 99, 132, 0.2)',
              'rgba(74,235,21,0.2)'
            ],
            borderWidth: 1,
            barPercentage: 1.0,
            categoryPercentage: 1.0
          },
          {
            label: '固定（資産・負債）',
            data: [this.FixedAssetsA / (this.FixedAssetsA + this.CurrentAssetsA), this.ixedLiabilitiesA / (this.CurrentLiabilitiesA + this.FixedLiabilitiesA + this.NetAssetsA), this.FixedAssetsB / (this.FixedAssetsB + this.CurrentAssetsB), this.ixedLiabilitiesB / (this.CurrentLiabilitiesB + this.FixedLiabilitiesB + this.NetAssetsB)],
            // backgroundColor: [
            //   'rgba(255, 99, 132, 0.2)',
            //   'rgba(74,235,21,0.2)'
            // ],
            borderWidth: 1,
            barPercentage: 1.0,
            categoryPercentage: 1.0
          },
          {
            label: '流動（資産・負債）',
            data: [this.CurrentAssetsA / (this.FixedAssetsA + this.CurrentAssetsA), this.NetAssetsA / (this.CurrentLiabilitiesA + this.FixedLiabilitiesA + this.NetAssetsA), this.CurrentAssetsB / (this.FixedAssetsB + this.CurrentAssetsB), this.NetAssetsB / (this.CurrentLiabilitiesB + this.FixedLiabilitiesB + this.NetAssetsB)],
            // backgroundColor: [
            //   'rgba(255, 99, 132, 0.2)',
            //   'rgba(74,235,21,0.2)'
            // ],
            borderWidth: 1,
            barPercentage: 1.0,
            categoryPercentage: 1.0
          }
        ]
      }
      this.options = {
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
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
