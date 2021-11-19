<template>
<div class="Task">
    {{todo.id}}
    {{todo.text}}
</div>
</template>

<script>
export default {
    props: [
        "todo"
    ]
}
</script>

<style>
.Task {
    width: 90%;
    height: 150px;
    border: solid white 1px;
    margin-right: auto;
    margin-left: auto;
    margin-top: 16px;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    align-content: center;
}
</style>