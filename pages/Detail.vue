<template>
    <div>
        <div class="content">
            <v-card class="cover" color="blue lighten-1">
                <v-card-title class="content-title">实验1</v-card-title>
                <v-card-text class="content-text">
                    同学们好，
                    本次实验主要目的是 掌握利用 SQL 语句定义、和简单操纵数据库的方法。
                    实验报告模板和实验指导书请参看附件。
                    rgds,
                    杜智华
                </v-card-text>
                <div class="space">附件</div>
                <v-card-text class="content-file">
                    <div>
                    <a :href="1234">实验1-实验报告模板2017.doc (64.5 KB)</a>
                    </div>
                    <div>
                    <a :href="1234">实验1-实验指导2017.doc (227.5 KB)</a>
                    </div>
                </v-card-text>
                <v-card-actions class="action">
                    <v-text-field v-if="showInput" class="input" :hide-details= "true" autofocus></v-text-field>
                    <v-spacer v-else></v-spacer>
                    <v-btn icon>
                        <v-icon color="grey">favorite</v-icon>
                    </v-btn>
                    <v-btn icon @click="comment">
                        <v-icon color="grey" v-on:click.native="comment">mode_comment</v-icon>
                    </v-btn>
                </v-card-actions>
            </v-card>
        </div>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '内容',
        showMenu: false,
        showBack: true,
        showLogo: false,
        actions: []
    });
    store.dispatch('appShell/appBottomNavigator/hideBottomNav');
}

export default {
    name: 'detail',
    metaInfo: {
        title: 'Home',
        titleTemplate: '%s - Lavas',
        meta: [
            {name: 'keywords', content: 'lavas PWA'},
            {name: 'description', content: '基于 Vue 的 PWA 解决方案，帮助开发者快速搭建 PWA 应用，解决接入 PWA 的各种问题'}
        ]
    },
    data(){
        return {
            showInput: false,
        }
    },
    methods: {
        comment(){
            this.showInput = true
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
.cover
    width 85%
    margin-top 10px
.action
    background-color white
    padding-top 0
    padding-bottom 2px
.content-title
    font-size 20px
.content-text
    text-align left 
    padding-top 0
.content-file
    word-break:break-all
    text-align left 
    padding-top 3px
.space 
    height 25px
    width 100%
    background-color #64B5F6
    text-align left 
    padding-left 15px
    line-height 25px
    color #757575
.input
    padding 0
</style>
