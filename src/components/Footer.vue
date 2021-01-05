<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span>item left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all">All</a></li>
            <li><a href="#/active">Active</a></li>
            <li><a href="#/complete">Complete</a></li>
        </ul>
        <button class="clear-completed">
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
        }
    }
</script>

<style  scoped>

</style>