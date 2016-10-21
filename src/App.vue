<template>
  <div id="app">
    <button  @click="book(1,'แล่ม1',100)">แล่ม 1</button>
    <button  @click="book(2,'แล่ม2', 100)">แล่ม 2</button>
    <button  @click="book(3,'แล่ม3', 100)">แล่ม 3</button>
    <button  @click="book(4,'แล่ม4', 100)">แล่ม 4</button>
    <button  @click="book(5,'แล่ม5', 100)">แล่ม 5</button>
    <button  @click="book(6,'แล่ม6', 100)">แล่ม 6</button>
    <button  @click="book(7,'แล่ม7', 100)">แล่ม 7</button><hr>
    <div v-for="show in data">
      {{show.name}} : จำนวน
      <button @click="book(show.id, show.name, show.price)">^</button>
      {{show.amount}}
      <button @click="delBook(show.id)">v</button> X 100 = {{show.amount * 1}}
      <button @click="del(show.id)">Delete</button><hr>
    </div>
    Total : {{sum}} <br>
    Discount : {{dis}} <br>
    xxx : {{sum - dis}}

  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  },
  methods: {
    book (id, name, price) {
      let index = this.data.findIndex(item => item.id === id)
      if (index >= 0 && index <= 6) {
        // console.log('มีแล่ม' + id + 'แล้ว')
        this.data[index].amount += 1
      } else {
        let addBook = {
          id: id,
          name: name,
          price: price,
          amount: 1
        }
        this.data.push(addBook)
      }
      // console.log(this.data)
      this.total()
      this.discount()
    },
    total () {
      var total = this.data.map(item => item.amount)
      this.sum = total.reduce((a, b) => a + b, 0) * 100
    },
    discount () {
      var count = this.data.map(item => {
        return { amount: item.amount, price: item.price }
      })
      console.log(count)
      this.dis = 0
      while (count.length > 1) {
        var sumprice = count.reduce((sum, count) => sum + count.price, 0)
        this.dis += ((count.length - 1) / 10) * sumprice
        count = count.map((item) => {
          return { amount: item.amount - 1, price: item.price }
        })
        count = count.filter((element) => element.amount !== 0)
      }
    },
    del (id) {
      let index = this.data.findIndex(item => item.id === id)
      this.data.splice(index, 1)
      this.total()
      this.discount()
    },
    delBook (id) {
      let index = this.data.findIndex(item => item.id === id)
      if ((this.data[index].amount - 1) < 1) {
        this.data.splice(index, 1)
      } else this.data[index].amount -= 1
      this.total()
      this.discount()
    }
  },
  data () {
    return {
      data: [],
      sum: 0,
      dis: 0
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
