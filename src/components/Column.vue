<template>
<div class="col">
    <div class="taskBtn">
        <input type="text" v-model="new_task_desc" />
        <button @click="addTask">Add task</button>
   </div>
    <div class="title">
        <span>{{columntitle}}</span>
    </div>
  <draggable v-model="tasks" group="tasks" @start="drag=true" @end="drag=false" @change="changed" :item-key="id" ghost-class="ghost" class="fill-height">
  <template #item="{element}">
    <task :todo="element" />
   </template>
   </draggable>
</div>
</template>

<script>
import draggable from 'vuedraggable'
import PouchDB from 'pouchdb-browser'
import task from '@/components/ColumnBox.vue'
export default {
    components: {draggable, task},
    props: [
          "columntitle",
    ],
    data() {
        return {
            new_task_desc : '',
            tasks: [],
            rev : '',
            drag : false,
        }
    },
    mounted() {
        this.loadFromPouch();
    },
    methods : {
        addTask() {
            var new_task = {
                id : 100,
                text : this.new_task_desc
            }
            this.tasks.push(new_task)
            this.new_task_desc = '';
            this.saveToPouch();
        },
        saveToPouch() {
            var db = new PouchDB("vue_kanbanBoard");
            db.put({
                _id: 'task_' + this.columntitle,
                _rev : this.rev,
                tasks : this.tasks
            }).then((Response) => {
                this.rev = Response.rev;
            });
        },
        loadFromPouch() {
            var db = new PouchDB("vue_kanbanBoard");
            db.get('task_' + this.columntitle).then(result => {
                this.tasks = result.tasks
                this.rev = result._rev
            })
            .catch( () => {} )
        },
        changed() {
            this.saveToPouch();
        }
    },
}
</script>

<style>
.col {
    color: rgb(0, 0, 0);
    width: 20%;
    display: inline-block;
    margin: 1%;
    vertical-align: top;
    padding-bottom: 25px;
    border: solid black 1px;
    height: 500px;
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
.ghost {
    opacity: 0.5;
}
.fill-height{
    height: 100%;
}
.taskBtn {
    margin-top: -25px;
}
.taskBtn>button {
    margin-left: 4px;
}
</style>