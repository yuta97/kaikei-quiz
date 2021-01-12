<template>
  <div id="app">
    <input v-model="FixedAssetsA">{{FixedAssetsA}}
    <button @click="showChart()" >グラフを作る</button>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <router-view/> -->
    <BarChart :FixedAssetsA="FixedAssetsA" :CurrentAssetsA="CurrentAssetsA" :CurrentLiabilitiesA="CurrentLiabilitiesA" :FixedLiabilitiesA="FixedLiabilitiesA" :NetAssetsA="NetAssetsA" :FixedAssetsB="FixedAssetsB" :CurrentAssetsB="CurrentAssetsB" :CurrentLiabilitiesB="CurrentLiabilitiesB" :FixedLiabilitiesB="FixedLiabilitiesB" :NetAssetsB="NetAssetsB" :chart-data="datacollection"/>
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
    datacollection: null
  }),
  mounted () {
      this.showChart()
  },
  methods: {
    showChart () {
      // this.loaded = false
      // console.log(this.FixedAssetsA)
      // this.FixedAssetsA = this.FixedAssetsA
      // this.loaded = true
      this.datacollection = {
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
          ]
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
