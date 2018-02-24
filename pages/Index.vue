<template>
    <div>
        <div class="content">
            <div v-for="n in 8" :key="n">
                <div class="card" @click="gotoDetail">
                    <div class="course">
                        计算机系统
                    </div>
                    <v-divider></v-divider>
                    <div class="add-content">
                        实验一
                        <v-icon large color="blue accent-3" class="icon">chevron_right</v-icon>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '新增',
        showMenu: true,
        showBack: false,
        showLogo: false,
        actions: [
            {
                icon: 'search',
                route: '/search'
            }
        ]
    });
    store.dispatch('appShell/appBottomNavigator/showBottomNav');
}

export default {
    name: 'index',
    metaInfo: {
        title: 'Home',
        titleTemplate: '%s - Lavas',
        meta: [
            {name: 'keywords', content: 'lavas PWA'},
            {name: 'description', content: '基于 Vue 的 PWA 解决方案，帮助开发者快速搭建 PWA 应用，解决接入 PWA 的各种问题'}
        ]
    },
    methods: {
        gotoDetail() {
            this.$router.push({path:'/Detail'})
        }
    },
    async asyncData({store, route}) {
        setState(store);
    },
    activated() {
        setState(this.$store);
    }
};
</script>

<style lang="stylus" scoped>
.content
    display flex
    justify-content center
    flex-direction column
    margin-bottom 50px
.card 
    width 80%
    height 100px
    text-align left 
    margin 10px auto
.course
    background-color #1976d2
    padding 15px
    border-radius 25px 25px 0 0
    color white
.add-content
    display flex
    justify-content space-between
    margin 10px 0 5px 15px
</style>
