<!-- 分栏布局 -->
<template>
 <div class="path_class">
   <el-button @click="a">收起</el-button>
   <el-menu
       :router="false"
       default-active="2"
       :collapse="collapse"
       :unique-opened="false"
       :collapse-transition="false"
   >
     <SubMenu :menu-list="subMenuList" />
   </el-menu>
 </div>
</template>

<script setup lang="ts" name="layoutColumns">
import { ref, computed, watch } from "vue";
import { useRoute } from "vue-router";
// import { useAuthStore } from "@/stores/modules/auth";
// import { useGlobalStore } from "@/stores/modules/global";
import SubMenu from "../../src/components/Menu/SubMenu.vue";
const collapse = ref(false)
const route = useRoute();
// const authStore = useAuthStore();
// const globalStore = useGlobalStore();
// const accordion = computed(() => globalStore.accordion);
// const isCollapse = computed(() => globalStore.isCollapse);
const menuList = ref([
  { path: '/vm', title: '云主机管理' },
  { path: '/desktop', title: '云桌面管理' },
  { path: '/cluster', title: '集群管理' },
  { path: '/node', title: '物理机管理' },
  { path: '/storage', title: '存储管理' },
  { path: '/image', title: '镜像管理' },
  // {k: '/backup',v: '备份和快照管理'},
  { path: '/user', title: '用户管理' },
  { path: '/system', title: '系统服务' }
]);
// const activeMenu = computed(() => (route.meta.activeMenu ? route.meta.activeMenu : route.path) as string);
const a = () => {
  collapse.value = !collapse.value
}
const subMenuList = ref([
  { path: '/vm', title: '云主机管理' },
  { path: '/desktop', title: '云桌面管理' },
  { path: '/cluster', title: '集群管理' },
  { path: '/node', title: '物理机管理' },
  { path: '/storage', title: '存储管理' },
  { path: '/image', title: '镜像管理' },
  // {k: '/backup',v: '备份和快照管理'},
  { path: '/user', title: '用户管理' },
  { path: '/system', title: '系统服务' }
]);
// const splitActive = ref("");
watch(
  () => [menuList, route],
  () => {
    // 当前菜单没有数据直接 return
    if (!menuList.value.length) return;
    // splitActive.value = route.path;
    const menuItem = menuList.value.filter((item:any) => {
      return true;
    });
    if (menuItem[0].children?.length) return (subMenuList.value = menuItem[0].children);
    console.log(subMenuList.value)
    // subMenuList.value = [];
  },
  {
    deep: true,
    immediate: true
  }
);
</script>

<style scoped lang="scss">
@import "./index.scss";
.path_class{
  position: fixed;
  top: 0;
  left: 0 ;
}
</style>
