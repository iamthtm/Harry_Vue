<template lang="html">
<div>
  Chart JS {{name}}<br>
  <canvas id="myChart" width="200px" height="50px"></canvas>
  {{r1}} <input type="range" v-model="r1">
  {{r2}} <input type="range" v-model="r2">
  {{r3}} <input type="range" v-model="r3">
  <button type="button" @click="add(this.name, r2, r3)">submit</button>
</div>
</template>

<script>
import Chart from 'chart.js'
export default {
  data () {
    return {
      r1: 30,
      r2: 40,
      r3: 50,
      data: []
    }
  },
  computed: {},
  mounted () {
    this.add(this.r1, this.r2, this.r3)
    var vm = this
    var loop = setInterval(function () {
      vm.add(this.name, this.r2, this.r3)
      vm.chart()
      console.log(loop)
    }, 5000)
  },
  methods: {
    chart () {
      var ctx = document.getElementById('myChart')
      var bar = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['1', '2', '3'],
          datasets: [
            {
              label: '# of Vote',
              data: this.data
            }]
        }
      })
      console.log(bar)
    },
    add (r1, r2, r3) {
      this.data[0] = r1
      this.data[1] = r2
      this.data[2] = r3
      this.chart()
    }
  },
  components: {},
  props: ['name']
}
</script>

<style lang="css">
#myChart {

}
</style>
