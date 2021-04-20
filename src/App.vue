<template>
  <div id="app">
    <table border="1" id="mytable" cellpadding="8" class="Shun-Shii" >
      <tr v-for="i in Math.floor(items.length/10)" :key="i">
        <td v-for="j in 10" :key="j" :ref="'a' + (10*(i-1)+(j-1))" :style="{ backgroundColor: '#fff', color: '#000'}">
          {{ items[10*(i-1)+(j-1)] }}
        </td>
      </tr>
    </table>
    <button class="btn" @click="draw">Thiu-Tshiam</button>
  </div>
</template>

<script>
import { stuList } from './data.js'

export default {
  name: 'app',
  data () {
    return {
      items: stuList,
      visit: new Array(stuList.length),
      temp: [],
      jumping: 6,
    }
  },
  mounted() {
    this.visit.fill(false)
  },
  methods: {
    async delay(delayMS) {
      return new Promise(resolve => {
        setTimeout( () => {
          resolve(2);
        }, delayMS);
      });
    },
    async draw() {
      while ( this.temp.length > 0 ) {
        let t = this.temp.pop();
        this.$refs['a' + t][0].style.backgroundColor = '#003865';
        this.$refs['a' + t][0].style.color = '#fff';
      }
      const valid = this.items.filter(it => it !== '').length;
      for ( let i=0; i<this.jumping; ++i ) {
        var x = Math.floor(Math.random() * valid);
        while ( this.visit[x] ) {
          x = Math.floor(Math.random() * valid);
        }
        this.$refs['a' + x][0].style.backgroundColor = '#93282c';
        this.$refs['a' + x][0].style.color = '#fff';
        await this.delay(400);
        if ( i < this.jumping-1 ) {
          this.$refs['a' + x][0].style.backgroundColor = '#fff';
          this.$refs['a' + x][0].style.color = '#000';
        }
      }
      this.temp.push(x);
      this.visit[x] = true;
    },
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
  font-size: 32px;
  padding: 1%;
  margin: 0;
}

.Shun-Shii {
  margin: 0px auto;
}

.btn {
  margin: 40px auto;
  font-size: 32px;
}
</style>
