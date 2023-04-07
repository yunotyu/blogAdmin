<!-- sideBar文件交接下的其他组件都是这个页面的子组件 -->
<!-- 这个是网页的左侧边栏 -->
<template>
  <div :class="{'has-logo':showLogo}">
    <!-- 是否显示logo,logo.vue组件 -->
    <logo v-if="showLogo" :collapse="isCollapse" />
    <!-- 滚动条，里面包裹着菜单项 -->
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <!-- ele ui的菜单控件 -->
      <el-menu
        :default-active="$route.path"
        :collapse="isCollapse"
        :background-color="variables.menuBg"
        :text-color="variables.menuText"
        :active-text-color="variables.menuActiveText"
        :collapse-transition="false"
        mode="vertical"
      >
        <!-- 单个菜单项 -->
        <!-- permission_routes用户可访问的路由集合 ，在getters.js可以看到用的是哪个属性-->
        <sidebar-item v-for="route in permission_routes" :key="route.path" :item="route" :base-path="route.path" />
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>

// Vuex状态管理的辅助函数mapGetters
import { mapGetters } from 'vuex'
import Logo from './Logo'
import SidebarItem from './SidebarItem'
import variables from '@/styles/variables.scss'

export default {
  components: { SidebarItem, Logo },
  computed: {
    // 是Vuex提供的将store中的getter映射到组件计算属性中的辅助函数
    ...mapGetters([
      'permission_routes',
      'sidebar'
    ]),
    showLogo() {
      return this.$store.state.settings.sidebarLogo
    },
    variables() {
      return variables
    },
    isCollapse() {
      return !this.sidebar.opened
    }
  }
}
</script>
