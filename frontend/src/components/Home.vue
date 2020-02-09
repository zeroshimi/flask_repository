<template>
  <div>
    <p>Home</p>
    <button @click="getRandom">占う</button>
    <p>Random number from backend: {{ randomNum }}</p>
    <h1 v-show="randomNum%4==0">Awesome!!!</h1>
    <h2 v-show="randomNum%4==1">Good</h2>
    <h3 v-show="randomNum%4==2">Bad...</h3>
    <h4 v-show="randomNum%4==3">S〇〇ks!!!</h4>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Home',
  data () {
    return {
      randomNum: 0
    }
  },
  methods: {
    getRandom () {
      this.randomNum = this.getRandomNum()
    },
    getRandomNum () {
      const path = 'http://localhost:5000/rand'
      axios.get(path)
        .then(response => {
          this.randomNum = response.data.randomNum
        })
        .catch(error => {
          console.log(error)
        })
    }
  },
  created () {
    this.getRandom()
  }
}
</script>
