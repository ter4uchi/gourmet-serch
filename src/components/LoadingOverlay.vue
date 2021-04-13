<template>
    <div v-show="isNotFriend" class="overlay">
        <h2 class="mozi">テラウチの知人ですか？</h2>
        <h4 class="mozi">※本アプリはテラウチの知人のみ利用を許可しています</h4>
        <input type="checkbox" @change="change" class="mozi"><span class="mozi">はい。知人です。</span>
    </div> 
</template>

<script >

export default {
    name:"LoadingOverlay",
    data(){
        return{
            isNotFriend:true
        }
    },
    created(){
        console.log(this.isNotFriend);
    },
    methods: {
        change(){
            this.isNotFriend = false;
        }
    }
}
</script>
<style scoped>
.overlay {
    position: fixed;
    top: 0;
    z-index: 100;
    width: 100%;
    height: 100%;
    background: rgba(100, 100, 100, 0.6);
}
.mozi{
    color: rgba(0,180,255,1);
}
</style>
