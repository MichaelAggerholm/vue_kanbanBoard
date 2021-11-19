<template>
    <div class="taskBox" @mouseover="mouseOver" @mouseleave="mouseOut">
        <div v-if="editMode">
            <textarea v-model="task_desc" @blur="saveTask" />
        </div>
        <div>
            {{todo.text}}
            <button class="editBtn" v-if="showEdit" @click="EditTask">edit</button>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        "todo"
    ],
    data() {
        return {
            showEdit : false, // Vis rediger knappen
            editMode : false, // rediger task tekst
            task_desc : ''
        }
    },
    methods : {
        mouseOver() {
            this.showEdit = true
        },
        
        mouseOut() {
            this.showEdit = false
        },
        EditTask() {
            this.editMode = true
            this.task_desc = this.todo.text
        },
        saveTask() {
            this.editMode = false
        }
    }
}
</script>

<style>
.taskBox {
    border: 1px solid gray;
    height: 150px;
    margin: 10px;
    padding: 15px;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-start;
    align-content: flex-start;
    background-color: rgb(214, 166, 108);
    border-radius: 2%;
}
</style>