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

    /*
     * 3. 在父组件中使用子组件 和 子组件向父组件发送数据（自定义事件v-on:自定义名称=‘自定义方法’）
     */
    <response v-on:subComponentSendDataToFatherComponent='acceptData'></response>
    <h2><strong>{{responseMsg}}</strong></h2>
    <h2><strong>{{dispatchData}}</strong></h2>

  </div>
</template>

<script>
import Storage from './storage';
/*
 * 1. 在父组件中引入子组件
 */
import greet from './components/greetFromAppComponent'
import response from './components/responseToAppComponent'

export default {
  data : function(){
    return　{
      'title'　:　'my　to　do　list',
      'taskList'　:　Storage.fetch(),
      'responseMsg' : '',
      'dispatchData'　:　''
    }
  },

  /*
   * 2. 在父组件中注册子组件
   */
  components : {greet, response},

  watch : {
    'taskList' : {
      handler : function(taskList){
        Storage.save(taskList);
      },
      deep : true
    }
  },
  /*
   * 1. 使用$dispatch()　方法发送数据,　子组件向父组件发送数据的方法
   */
  events　:　{
    'dispatchSendData'　:　function(msg){
      this.dispatchData　=　msg;
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
    },

    /*
     * 1. 使用　ｖ-on　和　$emit()　发送数据,　子组件向父组件发送数据的方法
     */
     acceptData : function(msg){
        this.responseMsg　=　msg
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
