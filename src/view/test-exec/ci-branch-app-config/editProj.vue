<template>
  <div>
    <card>
      <Menu mode="horizontal" :theme="menuTheme" :active-name="selectedMenu" @on-select="onMenuSelect">
        <Menu-Item name="baseConfig">
          <Icon type="ios-paper"/>
          内容管理
        </Menu-Item>
        <Menu-Item name="2">
          <Icon type="ios-people"/>
          用户管理
        </Menu-Item>
        <Submenu name="3">
          <template slot="title">
            <Icon type="ios-stats"/>
            统计分析
          </template>
          <MenuGroup title="使用">
            <Menu-Item name="3-1">新增和启动</Menu-Item>
            <Menu-Item name="3-2">活跃分析</Menu-Item>
            <Menu-Item name="3-3">时段分析</Menu-Item>
          </MenuGroup>
          <MenuGroup title="留存">
            <Menu-Item name="3-4">用户留存</Menu-Item>
            <Menu-Item name="3-5">流失用户</Menu-Item>
          </MenuGroup>
        </Submenu>
        <Menu-Item name="4">
          <Icon type="ios-construct"/>
          综合设置
        </Menu-Item>
      </Menu>
      <div>
       <span>利用router-link带参数： {{item}}</span>
        <base-config v-if="selectedMenu==='baseConfig'" :appBaseInfo="item"/>
      </div>
    </card>
  </div>

</template>

<script>
import baseConfig from './sub-pages/base-config'

export default {
  name: 'editProj',
  components: { baseConfig },
  props: ['item'],
  data () {
    return {
      menuTheme: 'light', // 主题
      selectedMenu: 'baseConfig', // 默认选中tab的name值
      // appBaseInfo: this.$route.params.tableItem
      appBaseInfo: 'hyx'
    }
  },
  methods: {
    onMenuSelect (name) {
      this.selectedMenu = name // Menu的select事件
      // this.appBaseInfo = this.currentData;
    }
  }
}
</script>

<style scoped>

</style>
