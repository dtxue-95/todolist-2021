<template>
    <footer class="footer">
        <span class="todo-count">
            <!-- <strong>{{todoNum<=1?"item":"items"}}</strong> -->
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum<=1">item left</span>
             <span v-else>items left</span>
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