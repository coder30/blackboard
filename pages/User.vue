<template>
    <div class="content">
        <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
                <v-card class="cover">
                    <v-card-media src="../static/img/background.jpg" height="300px">
                    <v-layout column class="media">
                        <v-spacer></v-spacer>
                        <v-card-title class="white--text pl-5 pt-5">
                        <div class="display-1 pl-5 pt-5">{{username}}</div>
                        </v-card-title>
                    </v-layout>
                    </v-card-media>
                    <v-list two-line>
                    <v-list-tile @click="login">
                        <v-list-tile-action>
                        <v-icon color="indigo">person</v-icon>
                        </v-list-tile-action>
                        <v-list-tile-content>
                        <v-list-tile-title>切换帐号</v-list-tile-title>
                        </v-list-tile-content>
                        <v-list-tile-action>
                        <v-icon>send</v-icon>
                        </v-list-tile-action>
                    </v-list-tile>
                    </v-list>
                </v-card>
                <v-card-text class="footer1">
                    &copy;2018 — <strong>cwf</strong>
                </v-card-text>
            </v-flex>
        </v-layout>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '我的',
        showMenu: true,
        showBack: false,
        showLogo: false,
        actions: []
    });
    store.dispatch('appShell/appBottomNavigator/showBottomNav');
}

export default {
    name: 'user',
    metaInfo: {
        title: 'Home',
        titleTemplate: '%s - Lavas',
        meta: [
            {name: 'keywords', content: 'lavas PWA'},
            {name: 'description', content: '基于 Vue 的 PWA 解决方案，帮助开发者快速搭建 PWA 应用，解决接入 PWA 的各种问题'}
        ]
    },
    data() {
        return {
            username:'curry'
        };
    },
    methods: {
        login(){
            this.$router.push({path:'/Login'})        
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
    height 100%
.cover
    border-radius 0
.footer1
    position absolute
    bottom 100px
    width 50%
    left 0
    right 0
    margin 0 auto
    text-align center
</style>
