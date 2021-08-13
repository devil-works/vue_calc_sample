<template>
  <div class="calc">
    <div class="bl_bmiChecker">
      <div><span>身長：</span><input v-model="height" type="number" class="hp_mb8">cm</div>
      <div><span>体重：</span><input v-model="weight" type="number"><span>kg</span></div>
      <div><button class="hp_mt8" @click="calculate">計算する</button></div>
      <div class="md-resWraper">
        <div v-if="result" class="el_res">BMI：{{result}}</div>
        <div v-if="err" class="hp_danger">{{err}}</div>
      </div>
      <table class="md-bmiLev">
        <thead>
          <tr>
            <th>BMI値</th>
            <th>判定</th>
          </tr>
        </thead>
        <tbody>
          <tr v-bind:class="{ active: isLow }">
            <td>18.5未満</td>
            <td>低体重(痩せ型)</td>
          </tr>
          <tr v-bind:class="{ active: is18 }">
            <td>18.5〜25未満</td>
            <td>普通体重</td>
          </tr>
          <tr v-bind:class="{ active: is25 }">
            <td>25〜30未満</td>
            <td>肥満(1度)</td>
          </tr>
          <tr v-bind:class="{ active: is30 }">
            <td>30〜35未満</td>
            <td>肥満(2度)</td>
          </tr>
          <tr v-bind:class="{ active: is35 }">
            <td>35〜40未満</td>
            <td>肥満(3度)</td>
          </tr>
          <tr v-bind:class="{ active: is40 }">
            <td>40以上</td>
            <td>肥満(4度)</td>
          </tr>
        </tbody>
      </table>
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
      isLow: false,
      is18: false,
      is25: false,
      is30: false,
      is35: false,
      is40: false,
    }
  },
  methods:{
    calculate(){
      this.isLow =false
      this.is18 =false
      this.is25 =false
      this.is30 =false
      this.is35 =false
      this.is40 =false

      if(this.height && this.weight){
         //BMI ＝ 体重kg ÷ (身長m)2
         //適正体重 ＝ (身長m)2 ×22
        const mHeight = this.height / 100
        const resCalc = this.weight / (mHeight * mHeight)
        this.result   = Math.round(resCalc * 100) /100;
        if(this.result < 18.5){
          this.isLow = true
        } else if (this.result > 18.5 && this.result < 25){
          this.is18 = true
        } else if (this.result >= 25 && this.result < 35){
          this.is25 = true
        } else if (this.result >= 35 && this.result < 40){
          this.is35 = true
        } else if (this.result >= 40){
          this.is40 = true
        }
        this.err= ''
      } else if (!this.weight && !this.height){
        this.err = "体重と身長を入力してください！"
      } else if (!this.height){
        this.err = "身長を入力してください！"
      } else {
        this.err = "体重を入力してください！"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
input[type="number"]::-webkit-outer-spin-button, 
input[type="number"]::-webkit-inner-spin-button { 
  -webkit-appearance: none; 
  margin: 0; 
} 
.active {
  color: #42b983;
}
.hp_danger {
  color: #ff4949;
}
.bl_bmiChecker {
  max-width: 720px;
  margin:auto;
}
.md-resWraper {
  margin: 32px 0;
  height: 32px;
}
.md-bmiLev {
  margin: 16px auto;
}
.el_res {
  color: #42b983;
  font-weight: bold;
  font-size: 18px;
}
.hp_mt8 {
  margin-top :8px;
}
.hp_mb8 {
  margin-bottom :8px;
}
</style>
