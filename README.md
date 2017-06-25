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

<<<<<<< HEAD
=======
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader)
>>>>>>> d101d1713807443838eb16873bec67e87dca84a1
