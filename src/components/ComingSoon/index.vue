<template>
    <div class="movie_body">
        <ul v-for="data in datalist" :key="data.filmId">
            <li>
                <div class="pic_show"><img :src="data.poster" :alt="data.name" @tap="handleToDetail(data.filmId)"></div>
                <div class="info_list">
                    <h2>{{data.name}}</h2>
                    <p>{{data.actors | actorFilter}}</p>
                </div>
                <div class="btn_pre">预售</div>
            </li>
        </ul>
    </div>
</template>

<script>
import Vue from 'vue'
Vue.filter('actorFilter',function(data){
    var arr = data.map(item=>item.name)
    arr = arr.join(',').split(',').slice(1).join(' ')
    // var newarr = arr.slice(1).join(' ')
    // console.log(newarr)
    return arr
})
export default {
    name:'ComingSoon',
    data(){
        return{
            datalist:[]
        }
    },
    mounted(){
        this.axios({
            url:'https://m.maizuo.com/gateway?cityId=310100&pageNum=1&pageSize=10&type=2&k=1826414',
            headers:{
                'X-Client-Info': '{"a":"3000","ch":"1002","v":"5.0.4","e":"1612017278652186488930305","bc":"310100"}',
                'X-Host': 'mall.film-ticket.film.list'
            }
        }).then(res=>{
            this.datalist = res.data.data.films
        })
    },
    methods:{
        handleToDetail(movieId){
            this.$router.push('/movie/detail/2/'+ movieId) //去创建动态路由
        }
    }
}
</script>

<style scoped>
    #content .movie_body{flex:1;overflow: auto;}
    .movie_body ul{margin:0 12px;overflow: hidden;}
    .movie_body ul li{margin-top:12px;display: flex;align-items: center;border-bottom:1px solid #e6e6e6;
    padding-bottom:10px}
    .movie_body .pic_show{width: 64px;height: 90px;}
    .movie_body .pic_show img{width: 100%;}
    .movie_body .info_list{margin-left:10px;flex:1;position: relative;}
    .movie_body .info_list h2{font-size: 17px;line-height: 24px;width: 150px;overflow: hidden;
    white-space: nowrap;text-overflow: ellipsis;}
    .movie_body .info_list p{font-size: 13px;color:#666;line-height: 22px;width: 200px;overflow: hidden;
    white-space: nowrap;text-overflow: ellipsis;}
    .movie_body .info_list .grade{font-weight: 700;color: #faaf00;font-size:15px;}
    .movie_body .info_list img{width: 50px;position: absolute;right: 10px;top:5px;}
    .movie_body .btn_mall,.movie_body .btn_pre{width: 47px;height: 27px;line-height: 28px;text-align:center;
    background-color: rgb(243, 130, 110);}
    .movie_body .btn_pre{background-color: #3c9fe6;}
</style>