<template>
    <div id="app">
        <v-app>
            <app-header
                class="app-shell-header"
                @click-menu="handleClickHeaderMenu"
                @click-back="handleClickHeaderBack">
            </app-header>
            <app-sidebar
                @hide-sidebar = "handleHideSidebar"
                @show-sidebar = "handleShowSidebar"
            >
            </app-sidebar>
            <transition
                :name="pageTransitionEffect"
                @before-enter="handleBeforeEnter"
                @after-enter="handleAfterEnter">
                <keep-alive v-if="$route.meta.keepAlive">
                    <router-view
                        :key="$route.fullPath"
                        class="app-view"
                        :class="[{'app-view-with-header': appHeaderShow}, pageTransitionClass]"
                        ></router-view>
                </keep-alive>
                <router-view
                    :key="$route.fullPath"
                    v-if="!$route.meta.keepAlive"
                    class="app-view"
                    :class="[{'app-view-with-header': appHeaderShow}, pageTransitionClass]"
                    ></router-view>
            </transition>
            <app-bottom-navigator
                class="app-shell-footer"
                @click-nav="handleClickBottomNav">
            </app-bottom-navigator>
        </v-app>
    </div>
</template>

<script>
import {mapState, mapActions} from 'vuex';
import AppHeader from '@/components/AppHeader';
import AppSidebar from '@/components/AppSidebar';
import UpdateToast from '@/components/UpdateToast';
import AppBottomNavigator from '@/components/AppBottomNavigator';

export default {
    name: 'app',
    components: {
        UpdateToast,
        AppHeader,
        AppSidebar,
        AppBottomNavigator
    },
    computed: {
        ...mapState('pageTransition', {
            pageTransitionType: state => state.type,
            pageTransitionEffect: state => state.effect
        }),

        ...mapState('appShell/appHeader', {
            appHeaderShow: state => state.show
        }),

        pageTransitionClass() {
            return `transition-${this.pageTransitionType}`;
        }
    },
    methods: {
        ...mapActions('appShell/appSidebar', [
            'showSidebar',
            'hideSidebar'
        ]),
        ...mapActions('appShell/common', [
            'setPageSwitching'
        ]),
        ...mapActions('appShell/appBottomNavigator', [
            'activateBottomNav'
        ]),
        handleBeforeEnter(el) {
            this.setPageSwitching(true);
        },
        handleAfterEnter(el) {
            this.setPageSwitching(false);
        },
        handleClickHeaderBack() {
            this.$router.go(-1);
        },
        handleClickHeaderMenu() {
            this.showSidebar();
        },
        handleHideSidebar() {
            this.hideSidebar();
        },
        handleShowSidebar() {
            this.showSidebar();
        },
        handleClickBottomNav({name}) {
            this.activateBottomNav(name);
        }
    }
};
</script>

<style lang="stylus">
@import '~@/assets/stylus/variable'
#app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50

    .app-view
        position absolute
        top 0
        right 0
        bottom 0
        left 0
        overflow-x hidden
        overflow-y auto

        &::-webkit-scrollbar
            width 0
            background transparent

        &.app-view-with-header
            top $app-header-height

        &.transition-slide
            transition transform 0.4s cubic-bezier(.55, 0, .1, 1)

            &.slide-left-enter
                transform translate(100%, 0)

            &.slide-right-enter
                transform translate(-100%, 0)

            &.slide-right-leave-active
                transform translate(100%, 0)

            &.slide-left-leave-active
                transform translate(-100%, 0)

        &.transition-fade
            opacity 1
            transition opacity 1s ease

            &.fade-enter
                opacity 0

            &.fade-leave-active
                opacity 0

        // &.transition-slide-fade
        //     &.slide-fade-enter-active
        //         transition: all .3s ease
        //
        //     &.slide-fade-leave-active
        //         transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0)
        //
        //     &.slide-fade-enter,
        //     &.slide-fade-leave-to
        //         transform: translateX(10px)
        //         opacity: 0
    .app-shell-footer
        position fixed
        bottom 0
        left 0
        right 0
</style>
