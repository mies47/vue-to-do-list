<template>
  <div id="app">
      <h1 class="header">My ToDo App</h1>
      <task-adder @task="addTask"></task-adder>
      <to-do-list :data-lists="{ completed ,pinned ,sortList}" @done="listItemDone" @pin="listItemPin"></to-do-list>
  </div>
</template>

<script>
import toDoList from './components/toDoList'
import taskAdder from './components/taskAdder'

export default {
  name: 'App',
  components: {
    toDoList,
    taskAdder
  },
  data:function(){
    return{
      completed:[],
      allTasks:[],
      pinned:[],
      sortList:[],
      index:0
    }
  },

  methods:{
      addTask:function(data){
          this.allTasks.push({...data , id:this.index});
          this.sortedList();
          this.index++;
      },
      compare:function(a , b){
          if(a.priority < b.priority) return 1;
          else if(a.priority > b.priority) return -1;
          else return 0;
      },
      listItemDone: function(id , isPinned){
          var completed = this.completed;
          if(isPinned){
              this.pinned = this.pinned.filter(function(item){
                  if(item.id === id)  completed.unshift(item);
                  return item.id !== id;
              });
          }else{
              this.allTasks = this.allTasks.filter(function(item){
                  if(item.id === id)  completed.unshift(item);
                  return item.id !== id;
              });
          }
          this.sortedList();
      },
      listItemPin: function(id , isPinned){
          var pinned = this.pinned;
          var allTasks = this.allTasks;
          if(isPinned){
              this.allTasks = this.allTasks.filter(function(item){
                  if(item.id === id)  pinned.unshift(item);
                  return item.id !== id;
              });
          }else{
              this.pinned = this.pinned.filter(function(item){
                  if(item.id === id)  allTasks.push(item);
                  return item.id !== id;
              });
          }
          this.sortedList();
      },
      sortedList(){
        this.sortList = this.allTasks.sort(this.compare);
      } 
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
