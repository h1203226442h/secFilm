<template>
    <div id="main">
        <Header Title="书信电影"/>
            <div id="content">
                <div class="movie_menu">
                    <router-link tag="div" class="city_name" to="/movie/city">
                        <span>{{$store.state.city.name}}</span><i class="iconfont icon-sanjiao"></i>
                    </router-link>
                    <div class="hot_switch">
                        <router-link tag="div" class="hot_item" to="/movie/nowplaying">正在热映</router-link>
                        <router-link tag="div" class="hot_item" to="/movie/comingsoon">即将上映</router-link>
                    </div>
                    <router-link tag="div" class="search_entry" to="/movie/search">
                        <i class="iconfont icon-sousuo"></i>
                    </router-link>
                </div>
                <keep-alive>
                    <router-view />
                </keep-alive>
            </div>
        <Tabbar />
        <router-view name="detail" />
    </div>
</template>

<script>
import Header from '@/components/Header'
import Tabbar from '@/components/Tabbar'
export default {
    name:'Movie',
    data(){
        return {
            cityname:''
        }
    },
    components:{
        Header,
        Tabbar
    },
    mounted(){
        this.cityname = localStorage.getItem('cityName')
    }
}
</script>

<style scoped>
    #content .movie_menu{width: 100%;height: 45px;border-bottom: 1px solid #e6e6e6;display: flex;
    justify-content: space-between;align-items: center;}
    .movie_menu .city_name{margin-left:20px;height: 100%;line-height: 45px;}
    .movie_menu .city_name.active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .city_name.router-link-active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .hot_switch{display: flex;height: 100%;line-height: 45px;}
    .movie_menu .hot_item{font-size: 15px;color:#666;width: 80px;text-align: center;margin:0 12px;
    font-weight: 700;}
    .movie_menu .hot_item.active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .hot_item.router-link-active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .search_entry{margin-right: 20px;height: 100%;line-height: 45px;}
    .movie_menu .search_entry.active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .search_entry.router-link-active{color:#ef4238;border-bottom: 2px solid #ef4238;}
    .movie_menu .search_entry i{font-size: 24px;color:#666}
</style>