<template>
  <div class="hello">
    <h1>子组件向父组件发送数据的方法使用</h1>
    <input　@click='sendData'　type='button'　value='向父组件发送数据'/>
    <input　@click='dispatch'　type='button'　value='dispatch向父组件发送数据'/>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: '使用　ｖ-on配合$emit()方法发送数据,　这是子组件给父组件发送的数据',
      dispatchData　:　'使用$dispatch()　方法发送数据,　子组件向父组件发送数据的方法'
    }
  },
  methods　: {
    sendData : function(){
      this.$emit('subComponentSendDataToFatherComponent',this.msg);
    },
    dispatch　:　function(){
      this.$dispatch('dispatchSendData',　this.dispatchData);
    }
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
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
