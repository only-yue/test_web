<template>
    <el-menu
            background-color="#545c64"
            text-color="#fff"
            active-text-color="#ffd04b"
            style="height: 100%;"
            :default-active="activeMenu"
            :collapse="isCollapse"
            :collapse-transition="false"
            router
    >
       <el-menu-item index="/Home">
           <i class="el-icon-s-home"></i>
           <span slot="title">首页</span>
       </el-menu-item>

        <el-menu-item :index="'/'+item.menuclick" v-for="(item,i) in menu" :key="i">
            <i :class="item.menuicon"></i>
            <span slot="title">{{item.menuname}}</span>
        </el-menu-item>

        <el-menu-item index="/Role" v-if="!hasRoleMenu">
            <i class="el-icon-s-check"></i>
            <span slot="title">角色管理</span>
        </el-menu-item>

    </el-menu>
</template>

<script>
    export default {
        name: "Aside",
        data(){
            return {
                //isCollapse:false

               /* menu:[
                    {
                        menuClick:'Admin',
                        menuName:'管路员管理',
                        menuIcon:'el-icon-s-custom'
                    },{
                        menuClick:'User',
                        menuName:'用户管理',
                        menuIcon:'el-icon-user-solid'
                    }
                ]*/
            }
        },
        computed:{
            "menu":{
                get(){
                    return this.$store.state.menu
                }
            },
            hasRoleMenu() {
                if (!this.menu || this.menu.length === 0) return false;
                return this.menu.some(item => 
                    item.menuclick === 'Role' || 
                    item.menuname === '角色管理');
            },
            // 根据当前路由路径设置活跃菜单项
            activeMenu() {
                // 获取当前路由路径
                const route = this.$route.path;
                return route;
            }
        },
        props:{
            isCollapse:Boolean
        }
    }
</script>

<style scoped>
/* 高亮显示的菜单项样式 */
.el-menu-item.is-active {
    background-color: #434a50 !important;
}
</style>