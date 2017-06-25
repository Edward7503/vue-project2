# my-vue-project

> this is my second vue project
子组件向父组件发送数据方法:
  1. v-on : 自定义属性 = ‘自定义方法’
  2. $emit()
  3. $dispatch()
  4. $boadcast()
使用方法:
  1. v-on 和 $emit()配合使用:
    在父组件中:
      1) <response v-on:subComponentSendDataToFatherComponent='acceptData'></response>
      2) methods　: {
            acceptData : function(msg){
               this.responseMsg　=　msg
            }
          }
      注意: *　使用　responseMsg　之前,先在　ｄata　数据中声明;　
      　　　*　msg　是从子组件发送过来的数据;　
      　　　*　v-on　的属性(subComponentSendDataToFatherComponent)要和子组件中$emit()方法的第一个参数一样　;

    在子组件中: 例如在点击事件中触发发送数据方法
      1)　<input　@click='sendData'　type='button'　value='向父组件发送数据'/>
      2)　methods　: {
           sendData : function(){
             this.$emit('subComponentSendDataToFatherComponent',this.msg);
           }
         }
    分析:　*　子组件发送数据　:　this.$emit('subComponentSendDataToFatherComponent',this.msg);
          *　父组件接收数据　:　acceptData　方法
          *　关联　:　subComponentSendDataToFatherComponent　属性
