<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
     <ol>
      <li>在父组件中<strong>引入</strong>子组件: import 变量名 form '子组件相对父组件的路径'</li>
      <li>在父组件中<strong>注册</strong>子组件: components:{组件名} </li>
      <li>在父组件中<strong>使用</strong>子组件: '<'greet'>''<'/greet'>' </li>
     </ol>
     <h1>{{sendDataToSubComponent}}</h1>
     <ol>
      <li>在父组件中给子组件发数据: sayHello='hello world!' </li>
      <li>在子组件中接受父组件的数据:  props:['sayHello'] </li>
      <li>在子组件中使用父组件发送的数据:  {{}} </li>
     </ol>

     <h1>子组件中给父组件发数据</h1>
          <ol>
           <li>v-on:自定义名称 </li>
           <li>$emit() </li>
           <li>$dispatch()</li>
           <li>$boadcast()</li>
          </ol>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: '在父组件中使用子组件'
    }
  },
  props : ['sendDataToSubComponent'],
  methods : function(){
    console.log(this.sendDataToSubComponent);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
