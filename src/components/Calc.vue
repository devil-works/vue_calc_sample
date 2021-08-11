<template>
  <div class="calc">
    <div class="bmi-maker">
      <div>身長:<input v-model="height" type="text">cm</div>
      <div>体重:<input v-model="weight" type="text">㎏</div>
      <div><button @click="calculate">計算する</button></div>
      <div v-if="err">{{err}}</div>
      <table>
        <thead>
          <tr>
            <th>BMI値</th>
            <th>判定</th>
          </tr>
        </thead>
        <tbody>
          <tr v-bind:class="{ active: is18 }">
            <td>18.5未満</td>
            <td>低体重(痩せ型)</td>
          </tr>
          <tr v-bind:class="{ active: is25 }">
            <td>18.5〜25未満</td>
            <td>普通体重</td>
          </tr>
          <tr v-bind:class="{ active: is30 }">
            <td>25〜30未満</td>
            <td>肥満(1度)</td>
          </tr>
          <tr v-bind:class="{ active: is35 }">
            <td>30〜35未満</td>
            <td>肥満(2度)</td>
          </tr>
          <tr v-bind:class="{ active: is40 }">
            <td>35〜40未満</td>
            <td>肥満(3度)</td>
          </tr>
          <tr>
            <td>40以上</td>
            <td>肥満(4度)</td>
          </tr>
        </tbody>
      </table>
      <div v-if="result">BMI：{{result}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BmiCalcular',
  data(){
    return{
      weight: '',
      height: '',
      result: '',
      err: '',
      is18: false,
      is25: false,
      is30: false,
      is35: false,
      is40: false,
    }
  },
  methods:{
    calculate(){
      //BMI ＝ 体重kg ÷ (身長m)2
      //適正体重 ＝ (身長m)2 ×22
      if(this.weight && this.height){
        const mHeight = this.height / 100
        const resCalc = this.weight / (mHeight * mHeight)
        this.result   = Math.round(resCalc * 100) /100;
        if(this.result < 18.5){
          this.is18 = true
        }
        this.err= ''
      } else if (!this.weight && !this.height){
        this.err = "体重と身長を入力してください！"
      } else if (!this.height){
        this.err = "身長を入力してください！"
      } else {
        this.err = "体重と身長を入力してください！"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bmi-maker{
  max-width: 1000px;
  margin:auto;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.active {
  color: #42b983;
}
</style>
