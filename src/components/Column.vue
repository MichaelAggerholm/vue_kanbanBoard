<template>
<div class="col">
    <div class="title">
        <span>{{columntitle}}</span>
    </div>
  <column-box v-for="todo in todos" v-bind:todo="todo" v-bind:key="todo.text"></column-box>
</div>
</template>

<script>
import ColumnBox from '@/components/ColumnBox.vue'
export default {
    components: {ColumnBox},
      name: 'Column',
      props: [
          "todos",
          "columntitle",
      ]
}
</script>

<style>
.col {
    color: rgb(0, 0, 0);
    height: 100%;
    width: 20%;
    display: inline-block;
    margin: 1%;
    vertical-align: top;
    padding-bottom: 25px;
    border: solid black 1px;
}
.col:nth-of-type(1) > div:not(:first-of-type) {
    background: #b1b1b1;
}
.col:nth-of-type(2) > div:not(:first-of-type) {
    background: #cf8f8f;
}
.col:nth-of-type(3) > div:not(:first-of-type) {
    background: #8fc6cf;
}
.col:nth-of-type(4) > div:not(:first-of-type) {
    background: #8fcfa0;
}
.title{
    margin-top: 20px;
    font-size: 120%;
    font-style: italic;    
}

.title span {
    top: -20px;
    width: 0; 
    height: 0; 
    border-left: 20px solid transparent;
    border-right: 20px solid transparent;
}
</style>