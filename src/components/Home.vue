<template>
  <h1>Kanban Board</h1>
    <Column :columntitle="'Backlog'"></Column>
    <Column :columntitle="'In progress'"></Column>
    <Column :columntitle="'Testing'"></Column>
    <Column :columntitle="'Done'"></Column>
</template>

<script>
import Column from '@/components/Column.vue'
export default {
    components: {
        Column
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