<template>
    <footer class="footer">
        <span class="todo-count">
            <!-- <strong>{{todoNum<=1?"item":"items"}}</strong> -->
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum<=1">item left</span>
             <span v-else>items left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all" @click="filterTodo('all')">All</a></li>
            <li><a href="#/active" @click="filterTodo('active')">Active</a></li>
            <li><a href="#/complete" @click="filterTodo('completed')">Complete</a></li>
        </ul>
        <button class="clear-completed" @click="clearCompleted">
            Clear completed
        </button>
    </footer>
</template>

<script>
    export default {
        name:"Footer",
        computed:{
            todoNum(){
                return this.$parent.todoDatas.filter((value)=>{
                    return !value.hasCompleted;
                }).length;
            }
        },
        methods:{
            filterTodo(childView){
                //处理函数用来改变父组件中的view值
                this.$parent.view=childView;
            },
            clearCompleted(){
                this.$parent.todoDatas=this.$parent.todoDatas.filter((value)=>{
                    return !value.hasCompleted;
                })
            }
        },
    }
</script>

<style  scoped>

</style>