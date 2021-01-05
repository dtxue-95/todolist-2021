<template>
    <li v-bind:class="{completed:todo.hasCompleted,editing:todo===editedTodo}">
        <div class="view">
            <input type="checkbox" class="toggle" v-model="todo.hasCompleted">
            <label @dblclick="editTodo(todo)">{{todo.value}}</label>
            <button class="destroy"
                @click="removeTodo(todo.id)"
            ></button>
        </div>
        <input type="text" class="edit"
            v-model.trim="editedTodo.value"
            v-focus="todo==editedTodo"
            @keyup.enter="doneTodo(index)"
            @blur="doneTodo(index)"
            @keyup.esc="cannelTodo(todo,index)"
        >
    </li>
</template>

<script>
    export default {
        name:"Item",
        props:['todo','index'],
        data(){
            return {
                editedTodo:"", //是否进入编辑状态的标识 editing
                value:""   //存储修改前的todo.value
            }
        },
        methods:{
            removeTodo(id){
                //this.$parent获取父组件对象,this.$root获取的是根组件对象
                this.$parent.todoDatas=this.$parent.todoDatas.filter((value)=>{
                    return !(value.id==id);
                });
            },
            editTodo(todo){
                this.value=todo.value; //进入编辑状态后之前的todo也存一份
                this.editedTodo=todo;
            },
            doneTodo(){
                this.editedTodo=""; //回车或失去焦点，恢复编辑状态
            },
            cannelTodo(todo,index){
                //将存储的以前传过来的todo.value,赋值给对应的todo的value
                this.$parent.todoDatas[index].value=this.value;
                this.editedTodo=""; //回车或失去焦点，恢复编辑状态
            }
        },
        directives:{
            //自定义指令v-focus
            focus(el){
                el.focus();
            }
        }
    }
</script>

<style  scoped>

</style>