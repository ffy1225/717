<template>
<div class="me">
    <header class="header">
        <span class="more"><i class="iconfont icon-shezhi"></i></span>
        <h1>我的717商城</h1>
    </header>
    <section class="scroll">
        <div class="banner">
            <h2><img src="src/assets/img/me/default_avatar.png" alt="default_avatar" @click="toLogin"></h2>
            <h3>{{$store.state.username}}</h3>
        </div>
        <div class="icons">
            <h1><img src="src/assets/img/me/my9.png" alt="">我的店铺 <i class="iconfont icon-xiangyoujiantou"></i></h1>
            <ul>
                <li v-for="(v, i) in icons " :key="i"><cite><img :src="v.src" alt=""></cite><span>{{v.cont}}</span></li>
            </ul>
        </div>
        <div class="list"> 
            <ul>
                <router-link v-for="(v, i) in list" :key="i" :to="{name: 'address'}" tag="li">
                    <cite><img :src="v.src" alt=""></cite>
                    <span>{{v.cont}}</span>
                    <i class="iconfont icon-xiangyoujiantou"></i>
                </router-link>
            </ul>
        </div>
    </section>
</div>
</template>

<script>
import { getCookie } from '../../utils/utils';
import jwt from 'jsonwebtoken';
export default {
    name: 'me',
    data () {
        return {
            icons: [
                {
                    src: 'src/assets/img/me/my1.png',
                    cont: '待付款'
                },
                {
                    src: 'src/assets/img/me/my2.png',
                    cont: '待发货'
                },
                {
                    src: 'src/assets/img/me/my3.png',
                    cont: '待收货'
                },
                {
                    src: 'src/assets/img/me/my4.png',
                    cont: '售后'
                },
                {
                    src: 'src/assets/img/me/my5.png',
                    cont: '我的订单'
                }
            ],
            list:[
                {
                    src: 'src/assets/img/me/my6.png',
                    cont: '我的社区'
                },
                {
                    src: 'src/assets/img/me/my7.png',
                    cont: '账户余额'
                },
                {
                    src: 'src/assets/img/me/my8.png',
                    cont: '地址管理'
                }
            ]
        }
    },
    methods: {
        toLogin () {
            this.$router.push({name: 'login'});
        }
    },
    created(){
        var token = getCookie('token');
        var that = this;
        jwt.verify(token, '1508', function (error, decoded) {
            if(error){
                that.$router.push({name: 'login'});
            }else{
                that.$store.commit('updated_username',{
                    username: decoded.telephone
                });
            }
        })
        
    }
};
</script>

<style scoped>
.me{
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
    display: -webkit-flex;
    flex-direction: column;
    font-size: 0.12rem;
}
.header{
    height: 0.9rem;
    position: relative;
}
.more{
    position: absolute;
    left: .3rem;
    top: .15rem;
    font-size: 0.4rem;
}
.header h1{
    font-size: 0.34rem;
    line-height: .9rem;
    text-align: center
}
.scroll{
    flex: 1;
    overflow-y: scroll;
    background: #eee;
}
.banner{
    height: 1.6rem;
    background: orange;
    text-align: center;
}
.banner h2 img{
    height: 1rem;
    width: 1rem;
    border-radius: 50%;
    margin-top: .1rem;
}
.banner h3 {
    font-size: 0.24rem;
    margin-top: .1rem;
}
.icons{
     background: #fff;
}
.icons h1{
    padding-left: .3rem;
    position: relative;
    font-size: 0.36rem;
    color: #fc4141;
    height: 1.72rem;
    line-height: 1.72rem;
    border-bottom: solid 1px #ccc;
}
.icons h1 img{
    width: .8rem;
    height: .8rem;
    margin-right: .18rem;
}
.icons h1 i{
    position: absolute;
    right: 0.3rem;
    top: 0.15rem;
    font-size: 0.3rem;
}
.icons ul {
    display: -webkit-flex;
    height: 1.48rem;
}
.icons ul li{
    flex: 1;
    text-align: center;
}
.icons ul li cite{
    display: block;
   
    text-align: center;
}
.icons ul li cite img{
    width: 0.4rem;
    height: 0.4rem;
    margin-top: .3rem;
    margin-bottom: 0.2rem;
}
.icons ul li span{
    font-size: 0.26rem;
    
}
.list{
    margin-top: 0.2rem;
    background: #fff;
}
.list ul li{
    padding-left: .3rem;
    padding-right: .3rem;
    border-bottom: solid 1px #ccc;
    height: 1rem;
    line-height: 1rem;
}
.list ul li cite img{
    width: 0.36rem;
    height: 0.36rem;
    margin-right: .3rem;
}
.list ul li span{
    font-size: 0.3rem;
}
.list ul li i{
    float: right;
}
</style>
