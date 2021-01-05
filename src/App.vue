<template>
  <section class="todoapp">
    <header class="header">
      <h1>Todos</h1>
      <input type="text" class="new-todo" placeholder="What?" 
      v-model="newTodo"
      @keyup.enter="addTodo"
      >
    </header>
    <section class="main">
      <input type="checkbox" class="toggle-all" v-model="isAll"/>
      <ul class="todo-list">
        <Item v-for="(value,index) in filterTodoDatas" v-bind:key="value.id" v-bind:index="index" v-bind:todo="value"/>
      </ul>
    </section>
    <Footer/>
  </section>
</template>

<script>
  import './css/index.css'
  import './css/base.css'
  import Item from './components/Item'
  import Footer from './components/Footer'
  export default {
    name:"App",
    components:{Item,Footer},
    data(){
      return {
        todoDatas:[], //存储所有的todo
        newTodo:"", //存储添加新的todo.title
        view:"all", //过滤数据属性默认all
      }
    },
    methods:{
      addTodo(){
        
        //如果是react的话 就用 if(e.keyCode!==13) return false;
        //在vue中只需要使用键名修饰符即可 @keyup.enter = "addTodo"
        if(this.newTodo=="") return false;   //做一个控制 如果添加内容为空 不能回车
        let todo={};
        todo.id=new Date().getTime();
        todo.value=this.newTodo;
        todo.hasCompleted=false;
        this.todoDatas.push(todo);
        this.newTodo="";
      }
    },
    computed:{
      isAll:{
        get(){
          return this.$children.todoNum==0;
        },
        set(value){
          this.todoDatas.map((todo)=>{
            todo.hasCompleted=value;
            return todo;
          })
        }
      },
      filterTodoDatas(){
        //计算属性显示过滤数据
        switch(this.view){
          case "all":
            return this.todoDatas;
          case "active":
            return this.todoDatas.filter((value)=>{
              return !value.hasCompleted;
            });
          case "completed":
            return this.todoDatas.filter((value)=>{
              return value.hasCompleted;
            });
            default:
              return this.todoDatas;
        }
      }
    }
  }
</script>

<style scoped>

</style>
