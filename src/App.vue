<template>
  <div id="app">
    <table border="1" id="mytable" cellpadding="8" class="Shun-Shii" >
      <tr v-for="i in 6" :key="i">
        <td v-for="j in 10" :key="j" :ref="'a' + (10*(i-1)+(j-1))" :style="{ backgroundColor: '#fff', color: '#000'}">
          {{ items[10*(i-1)+(j-1)] }}
        </td>
      </tr>
    </table>
    <button class="btn" @click="draw">Thiu-Tshiam</button>
  </div>
</template>

<script>
var stuList = ['王芷鈴', '何昀潔', '何芷倩', '周承佑', '林冠宇', '施育衡', '涂家銓', '高子翔', '康馨儒', '陳采藜', '陳宥圻', '陳捷文', '謝尚恆', '呂穎衡', '林士傑', '林廷威', '紀軒宇', '張心瑜', '陳威宇', '劉柏顯', '盧　萱', '陳兆閔', '莊博傑', '方　元', '朱自宇', '李佳芸', '林俊誠', '陳昱如', '楊昊翰', '蔡鳳駿', '王瑞渝', '王麒翔', '張　芩', '連庭萱', '彭建霖', '葉淯鎔', '蕭　瀜', '徐梓豪', '蕭于傑', '于子緯', '鐘子淳', '沈子龢', '陳映達', '盧昭華', '張　煜', '林遠邦', '劉子弘', '陳映澄', '林宥宏', '黃　瀚', '李奕慧', '洪菀妤', '', '', '', '', '', '', '', ''];
var visit = new Array(52);
for ( let i=0; i<52; ++i )  visit[i] = false;

export default {
  name: 'app',
  data () {
    return {
      items: stuList,
      temp: []
    }
  },
  components: {
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
      for ( let i=0; i<6; ++i ) {
        var x = Math.floor(Math.random() * 52);
        while ( visit[x] ) {
          x = Math.floor(Math.random() * 52);
        }
        this.$refs['a' + x][0].style.backgroundColor = '#93282c';
        this.$refs['a' + x][0].style.color = '#fff';
        await this.delay(500);
        if ( i < 5 ) {
          this.$refs['a' + x][0].style.backgroundColor = '#fff';
          this.$refs['a' + x][0].style.color = '#000';
        }
      }
      this.temp.push(x);
      visit[x] = true;
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
