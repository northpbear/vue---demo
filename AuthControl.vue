<script>
  import { getAuth } from "@/api/xxx.xxx.xxx.a"
  export default {
    name: "AuthControl",
    //表示这是一个函数式组件
    functional: true,
    props: {
      //在调用组件时需要给组件绑定的参数，被组件包裹的DOM需要是其中包含的权限角色才能访问
      auth: {
        type: Array,
        request: true
      }
    },
    //vue提供的不使用template的渲染方式，因为要控制组件内部的solt是否渲染，template不方便操作
    //当functional: true的时候，组件是无状态的也是无实例的，无法使用this传参，官方提供了context用于数据的传递
    // eslint-disable-next-line no-unused-vars,vue/require-render-return
    render(createElement, context) {
      //从服务器获取当前的权限
      const currentAuth = getAuth();
      //解构赋值，props和scopedSlots是vue提供的字段，可以从context对象中获取相应的数据
      let { props, scopedSlots } = context;
      //判断绑定的权限是否包含当前权限，有则渲染默认插槽内容，没有则为空
      props.auth.includes(currentAuth) ? scopedSlots.default() : null;
    }
  }
</script>

