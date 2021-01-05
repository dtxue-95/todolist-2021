<template>
    <li v-bind:class="{completed:todo.hasCompleted}">
        <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.hasCompleted">
            <label>{{todo.value}}</label>
            <button class="destroy"
                @click="removeTodo(todo.id)"
            ></button>
        </div>
        <input type="text" class="edit">
    </li>
</template>

<script>
    export default {
        name:"Item",
        props:['todo'],
        methods:{
            removeTodo(id){
                //this.$parent获取父组件对象,this.$root获取的是根组件对象
                this.$parent.todoDatas=this.$parent.todoDatas.filter((value)=>{
                    return !(value.id==id);
                });
            }
        }
    }
</script>

<style  scoped>

</style>