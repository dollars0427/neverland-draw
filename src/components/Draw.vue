<template>
  <div class="wrapper">
    <h1>NEVERLAND抽卡系統</h1>
    <div class="message">
      試營運中。如果有BUG請回報葉慈（不過真的會有我以外的人用嗎？）
    </div>
    <div class="form-group row">
      <label class="col-form-label">輸入角色名：</label>
      <div>
        <input v-model="name" class="form-control" type="text" value="">
      </div>
    </div>
    <div class="action-buttons">
      <button class="btn btn-primary" v-on:click="draw">
        單抽
      </button>
      <button class="btn btn-primary" v-on:click="drawTen">
        十連抽
      </button>
    </div>

    <div class="result" v-if="results.length !== 0 ">
      <h2>{{ name }}的抽卡結果為：</h2>
      <ul class="items">
        <li v-for="result in results">
          {{ result.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import pool from '../assets/pool.json';
export default {
  name: 'Draw',
  data(){
    return {
      name: '',
      poolItems: [],
      results: [],
    };
  },
  methods: {
    draw(){
      //Clear result
      this.results = [];
      const items = this.poolItems;
      const result = items[Math.floor(Math.random() * items.length)];
      this.results.push(result);
    },
    drawTen(){
      //Clear result
      this.results = [];
      let items = this.poolItems;
      for(let i = 0; i < 10; i++){
        const result = items[Math.floor(Math.random() * items.length)];
        this.results.push(result);
      }
    },
    shuffle(arr) {
      var i = arr.length, t, j;
      while (i) {
        j = Math.floor(Math.random() * i--);
        t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
      }
    },
  },
  created(){
    const items = pool.items;
    items.forEach(function(item){
      for(let i = 0; i < item.number; i++){
        items.push(item);
      }
    });
    this.shuffle(items);
    this.poolItems = items;
  },
}
</script>

<style scoped>
.wrapper{
  padding: 1em;
}
.message{
  margin-top: 1em;
  margin-bottom: 1em;
}
.form-group{
  margin-left: 0;
}
.result{
  margin-top: 50px;
}
.items{
  padding: 0;
  list-style-type: none;
}
</style>
