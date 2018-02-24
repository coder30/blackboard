<template>
    <div id="abc">
        <div class="content">
            <img src="../static/img/icons/Blackboard_Inc._logo.png" class="icon" />
            <v-form class="login">
                <v-text-field prepend-icon="person" name="login" label="学号" type="text" @click="focusText" v-model="account"></v-text-field>
                <v-text-field prepend-icon="lock" name="password" label="密码" id="password" type="password" @click="focusText" v-model="password"></v-text-field>
            </v-form>
            <v-btn large color="primary" class="submit" @click="signIn">登录</v-btn>
        </div>
    </div>
</template>

<script>
import {mapState, mapActions} from 'vuex';
import AppBottomNavigator from '@/components/AppBottomNavigator';
function setState(store) {
    store.dispatch('appShell/appHeader/setAppHeader', {
        show: true,
        title: '',
        showMenu: false,
        showBack: false,
        showLogo: false
    });
}
export default {
    name: 'login',
    data() {
        return{
            account: '',
            password: ''
        }
    },
    methods: {
        focusText(){
            var div = document.getElementById('abc')
            div.scrollTop = div.scrollHeight
            setTimeout(() => {
                div.scrollTop = div.scrollHeight
            }, 100);
        },
        signIn(){
            console.log(this.account)
            console.log(this.password)

        }
    },
    async asyncData({store, route}) {
        setState(store);
    },
    activated() {
        setState(this.$store);
    },
    created() {
        this.$store.dispatch('appShell/appBottomNavigator/hideBottomNav');
    }
};
</script>

<style lang="stylus" scoped>
.content
    display flex
    justify-content center
    flex-wrap wrap
    flex-direction:column
.icon 
    width: 120px
    height: 120px
    margin 20% auto
.login
    width 80%
    margin auto
.white-block
    height 100px
.submit
    width 30%
    margin auto
</style>
