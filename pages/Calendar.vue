<template>
    <div>
        <div class="content">
            <v-date-picker
                v-model="date"
                event-color="blue lighten-4"
                :full-width="true"
                :no-title="true"
                :scrollable="true"
                :events="functionEvents"
                class="calendar"
            ></v-date-picker>
            <div class="space">作业</div>
            <div class="event">
                <div @click="gotoDetail">
                <event-card v-for="n in 1" :key="n" class="card"></event-card>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import {mapActions} from 'vuex';
import EventCard from '@/components/EventCard';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '日历',
        showMenu: true,
        showBack: false,
        showLogo: false,
        actions: []
    });
    store.dispatch('appShell/appBottomNavigator/showBottomNav');
}

export default {
    name: 'calendar',
    components: {
        EventCard
    },
    data() {
        return {
            arrayEvents: null,
            date: '',
        }
    },
    methods: {
        functionEvents (date) {
            const [,, day] = date.split('-')
            return parseInt(day, 10) % 3 === 0
        },
        gotoDetail() {
            this.$router.push({path:'/detail'})
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
    height 100%
    flex-wrap wrap
.space 
    height 25px
    width 100%
    background-color #BBDEFB
    text-align left 
    padding-left 15px
    line-height 25px
    color #757575
.event
    width 100%
    margin-bottom 50px
    margin-left 30px
.card
    margin-bottom 20px
</style>
