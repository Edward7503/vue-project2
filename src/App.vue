<template>
  <div id="app">
    <h3>{{title}}</h3>
    <input @keyup.enter='addTask' v-model='newTask' type='text' name='myTask'/>
    <input @click='addTask' type='submit' value='提交'/>
    <ul>
      <li @click='checkOut(item)' :class='{ finished : item.isFinished }' v-for='item in taskList' v-html='item.task'></li>
    </ul>

    /*
     * 3. 在父组件中使用子组件 和 向子组件发送数据（sendDataToSubComponent='hello, 父组件给子组件发送的数据'）
     */
    <greet sendDataToSubComponent='父组件给子组件发送的数据'></greet>
  </div>
</template>

<script>
import Storage from './storage';
/*
 * 1. 在父组件中引入子组件
 */
import greet from './components/greetFromAppComponent'
export default {
  data : function(){
    return　{
      'title'　:　'my　to　do　list',
      'taskList'　:　Storage.fetch()
    }
  },
  /*
   * 2. 在父组件中注册子组件
   */
  components : {greet},
  watch : {
    'taskList' : {
      handler : function(taskList){
        Storage.save(taskList);
      },
      deep : true
    }
  },
  methods : {
    addTask : function(){
      if(this.newTask){
        this.taskList.push(
          {
            'task'　:　this.newTask,
            'isFinished'　:　false,
            'oldValue' : '',
            'once' : true
          }
        )
        this.newTask = '';
      }
    },
    checkOut : function(item){
      item.isFinished  = !item.isFinished;
      if(item.once){
        item.oldValue = item.task;
        item.once = false;
      }
      if(item.isFinished){
        item.task = '<del>'+ item.task +'</del>'
      }else{
        item.task = '';
        item.task = item.oldValue;
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished {
  color: #c0c0c0;
}
</style>
