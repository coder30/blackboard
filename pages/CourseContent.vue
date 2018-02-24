<template>
    <div>
        <v-tabs
            v-model="active"
            color="blue"
            dark
            slider-color="yellow"
            grow
            class="tab"
            >
            <v-tab
                v-for="tab in tabs"
                :key="tab"
                ripple>
                {{ tab }}
            </v-tab>
            <v-tab-item
                v-for="num in 4"
                :key="num"
                class="tab-page"
            >
                <div v-for="n in 4" :key=n class="content">
                    <event-card v-if="num==1" @click.native="gotoDetail" type="homework"></event-card>
                    <event-card v-if="num==2" @click.native="download" type="plan"></event-card>
                    <event-card v-if="num==3" @click.native="download" type="grade"></event-card>
                    <event-card v-if="num==4" @click.native="download" type="homework"></event-card>
                </div>
            </v-tab-item>
        </v-tabs>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
import EventCard from '@/components/EventCard';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '计算机系统',
        showMenu: false,
        showBack: true,
        showLogo: false,
    });
    store.dispatch('appShell/appBottomNavigator/hideBottomNav');
}

export default {
    name: 'course-content',
    components: {
        EventCard,
    },
    data() {
        return {
            active: null,
            tabs:['作业','教案','成绩','通知'],
            tab: ''
        }
    },
    methods: {
        gotoDetail() {
            this.$router.push({path:'/detail'})
        },
        download() {
            
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
.tab
    height :100%
.content
    display flex
    justify-content center
    margin 15px
    height 100%
</style>
