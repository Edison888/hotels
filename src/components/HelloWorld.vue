<template>
  <div class="page-search">
      <div class="search-city">
        <div class="search-city-title">
          <div class="bar bar-nav flight-order-head" style="opacity: 14.24;">
            <a class="icon icon-left-nav pull-left icon-back tjclick" data-rel="back" ></a>
            <h1 class="title">2018葛洲坝公司协议酒店</h1>
          </div>
        </div>
        <ul class="search-city-list">
          <!-- 延迟加载 -->
          <li v-for="(city, index) in hotelsList" :key="index" class="city1">
            <router-link  :to="{path:'/details',query: {id:index} }">
              <div><h2>{{city.name}}</h2><p>共有<span>{{city.hotels.length}}</span>家酒店</p><i class="icon-left"></i></div>
            </router-link></li>
        </ul>
      </div>
    </div>
</template>

<script>
const ERR_OK = 0
export default {
  name: 'App',
  data () {
    return {
      hotelsList: []
    }
  },
  created () {
    this.$http.get('./api/hotels').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.hotelsList = response.data
        console.log(this.hotelsList)
      }
    })
  }
}
</script>

<style>
  #app {

  }
  .search-city-list {
    padding: 0 4px;
  }
  .page-search .search-city .search-city-title {
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .page-search p {
    color: #555;
  }
  .page-search .search-city .search-city-list li {
    height: 75px;
    margin-bottom: 4px;
    overflow: hidden;
    position: relative;
  }
  .page-search .search-city .search-city-list li.city1 {
    background: url(//m.elongstatic.com/static/webapp/hotel/img/search/citys.jpg) 0 0;
    background-size: 100% 750px;
  }
  .page-search .search-city .search-city-list li div {
    padding: 0 24px;
    display: block;
    height: 75px;
    overflow: hidden;
  }
  .page-search .search-city .search-city-list li h2 {
    color: #FFF;
    text-shadow: 1px 1px 6px #000;
    font-size: 1.5rem;
    font-weight: normal;
    margin-top: 16px;
    margin-bottom: 6px;
  }
  .page-search .search-city .search-city-list li p {
    font-size: .813rem;
    color: #FFF;
  }
  .page-search .search-city .search-city-list li p span {
    color: #F55;
  }
  .page-search .search-city .search-city-list li .icon-left {
    display: block;
    position: absolute;
    top: 50%;
    margin-top: -9px;
    width: 14px;
    height: 14px;
    border: 1px solid #FFF;
    border-width: 0 0 2px 2px;
    -webkit-transform: rotate(-135deg);
    -ms-transform: rotate(-135deg);
    transform: rotate(-135deg);
    right: 10px;
  }
  .bar {
    position: relative;
    z-index: 10000;
    height: 44px;
    padding-right: 10px;
    padding-left: 10px;
    background-color: #fff;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    left: 0px;
    right: 0px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
  .bar-nav {
    background-color: #fcfcfc;
    color: #444;
    box-shadow: 0px 1px 2px #ddd;
  }
  .pull-left {
    float: left;
  }
  .bar .icon {
    position: relative;
    z-index: 20;
    width: 34px;
    height: 44px;
    display: inline-block;
    line-height: 44px;
    font-size: 24px;
    color: #fff;
    padding-top: 3px;
  }
  .bar .icon-back {
    color: #858585;
    margin-left: -10px;
    padding-left: 10px;
  }
  .title {
    position: absolute;
    display: block;
    width: 100%;
    padding: 0;
    margin: 0 -10px;
    font-size: 1.2rem;
    font-weight: bold;
    line-height: 44px;
    text-align: center;
    white-space: nowrap;
  }
</style>
