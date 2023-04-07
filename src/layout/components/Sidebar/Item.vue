<!-- item 组件通过定义 render 函数完成组件渲染 -->
<script>
export default {
  name: 'MenuItem',
  functional: true,
  props: {
    icon: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    }
  },
  // render函数的作用是，将h创建的Node节点信息return返回给
  // Vue.js底层处理文件中的beforeMount()生命周期钩子函数，让其将Node节点信息在界面中渲染出来.
  // h参数是一个createElement函数，用于创建节点信息，其内有三个参数h(‘el’,‘css’,vnodeArr)
  // 其中，el表示当前节点的标签，比如可以是div、span等；css是当前节点标签的css样式；vodeArr是当前节点标签中的子标签，指的是比如：如下div节点中的span标签.
  // context参数代表当前节点下的所有信息，使用场景：在需要对当前节点中子标签进行改动时，
  // 使用context.slots.default 拿到当前节点下所有的子节点信息，这些信息是以数组形式存储的，
  // 可以通过数组的方式找到相应的Node节点，然后对其进行修改。如下是对context.slots信
  render(h, context) {
    const { icon, title } = context.props
    const vnodes = []

    if (icon) {
      vnodes.push(<svg-icon icon-class={icon}/>)
    }

    if (title) {
      vnodes.push(<span slot='title'>{(title)}</span>)
    }
    return vnodes
  }
}
</script>
