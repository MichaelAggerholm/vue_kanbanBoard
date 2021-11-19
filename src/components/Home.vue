<template>
  <h1 v-on:click="test">Kanban Board</h1>
  <Column v-on:click="dropToInProgress" v-bind:todos="arrBacklog" :columntitle="'Backlog'"></Column>
  <Column v-on:click="dropToTesting" v-bind:todos="arrInProgress" :columntitle="'In progress'"></Column>
  <Column v-on:click="dropToDone" v-bind:todos="arrTesting" :columntitle="'Testing'"></Column>
  <Column v-bind:todos="arrDone" :columntitle="'Done'"></Column>
</template>

<script>
import Column from '@/components/Column.vue'
export default {
  components: {
      Column,
      },
    data() {
        return {
            drag: false,
            arrBacklog: [
                {id: 1, text: "Backlog 1"},
                {id: 2, text: "Backlog 2"},
                {id: 3, text: "Backlog 3"},
                {id: 4, text: "Backlog 4"},
            ],
            arrInProgress: [
                {id: 5, text: "In Progress 1"},
                {id: 6, text: "In Progress 2"},

            ],
            arrTesting: [
                {id: 7, text: "Testing 1"},
                {id: 8, text: "Testing 2"},

            ],
            arrDone: [
                {id: 9, text: "Done 1"},

            ]
        }
    },
    methods: {
        dropToInProgress(){
            var temp = this.arrBacklog.pop()
            this.arrInProgress.push(temp)
        },
        dropToTesting(){
            var temp = this.arrInProgress.pop()
            this.arrTesting.push(temp)
        },
        dropToDone(){
            var temp = this.arrInProgress.pop()
            this.arrDone.push(temp)
        }
    }
}
</script>

<style>
body{
    background: #fff;
    background-repeat: no-repeat;
    background-size: cover;
}
</style>