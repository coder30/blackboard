<template>
    <div class="item">
        <div class="edge"></div>
        <div class="title">
            实验一
        </div>
        <div v-if="type=='homework'">
            <div class="arrow">
                <v-icon large color="blue accent-3" class="icon">chevron_right</v-icon>
            </div>
        </div>
        <div v-if="type=='plan'">
            <div class="arrow">
                下载
                <v-icon medium color="blue accent-3" class="icon">file_download</v-icon>
            </div>
        </div>
        <div v-if="type=='grade'">
            <div class="grade">
                90.00
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'eventCard',
    props: {
        text: {
            type: String,
            default: '站点发生更新，请手动刷新'
        },
        type: ''
    },
    data() {
        return {
            show: false
        };
    },
    mounted() {
        window.addEventListener('sw.update', this.handleUpdate);
    },
    beforeDestroy() {
        window.removeEventListener('sw.update', this.handleUpdate);
    },
    methods: {
    }
};
</script>

<style lang="stylus" scoped>
.item
    background #F5F5F5
    display flex
    border 1px 
    border-radius 5px 
    width 80%
    height 45px
    align-items center
    box-shadow: 3px 3px 3px #E0E0E0
.title 
    margin-left 10px
    margin-right auto
.edge
    width 5px
    height 100%
    background-color #1976d2
    border-radius 4px 0px 0px 4px
.grade
    margin-right 20px
</style>
