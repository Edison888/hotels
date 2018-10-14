<template>
<div class="detail-mainNew type">
  <ul>
    <li v-for="(hotel, index) in  hotels" :key="index"  :class="scopesDefault[index]?'on rooms':'off  rooms'"  @click="changeStatus(index)">
      <div class="wrap ">
        <div class="left   tjclick">
          <div class="pic tjclick rpDetail">
            <img  :src="hotel.img" />
          </div>
          <div class="picroom-info">
            <div class="room">
              {{hotel.name}}
            </div>
            <div class="room-info">
              <span>总机：{{hotel.phone}}</span>
            </div>
            <div class="room-info">
              <span>地址：{{hotel.adress}}</span>
            </div>
            <div class="room-info">
              <span>距英皇中心距离：{{hotel.distance}}</span>
            </div>
          </div>
        </div>
        <div class="de-btn">
          <i></i>
        </div>
      </div>
      <div class="info-list" v-if="scopesDefault[index]">
        <ul>
          <li  v-for="(room, index) in  hotel.roomtype" :key="index" >
            <div class="left tjclick">
              <div class="bra clearfix">
                {{room.name}}
              </div>
              <div class="xstm">
                <span class="suppliername">付费早餐：{{hotel.breakfast}}</span>
              </div>
              <div class="act">
                <span class="tag" style="color:#4499ff;border: 1px solid #4499ff;">楼层：{{room.floor}}</span>
              </div>
            </div>
            <div class="value">
              <div class="price">
                &yen;
                <span>{{room.price}}</span>
              </div>
            </div>
          </li>
        </ul>
      </div> </li>
  </ul>
</div>
</template>

<script>
const ERR_OK1 = 0
export default {
  name: 'details',
  data () {
    return {
      id: 0,
      hotelsList: [],
      hotels: [],
      scopesDefault: []
    }
  },
  methods: {
    changeStatus (index) {
      console.log(index)
      if (this.scopesDefault[index] === true) {
        this.$set(this.scopesDefault, index, false)
      } else {
        this.$set(this.scopesDefault, index, true)
      }
      console.log(this.scopesDefault)
    }
  },
  created: function () {
    this.id = this.$route.query.id
    this.$http.get('./api/hotels').then((response) => {
      response = response.body
      if (response.errno === ERR_OK1) {
        this.hotelsList = response.data
        this.hotels = this.hotelsList[this.id].hotels
        console.log(this.hotels)
      }
    })
  }
}
</script>

<style>
  .detail-mainNew  ul li {
    background: #FFF;
    border-top: 1px solid #ebebeb;
    border-bottom: 1px solid #ebebeb;
    margin-bottom: 8px;
    position: relative;
    width: 100%;
    overflow: hidden;
    width: 100%;
    margin-bottom: 0;
  }

  .detail-mainNew  ul li .wrap {
    position: relative;
    overflow: hidden;
    padding: 14px 40px 14px 12px;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -moz-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -moz-box-align: center;
    -ms-flex-align: center;
    -webkit-box-pack: center;
    -moz-box-pack: center;
    -ms-flex-pack: center;
    -webkit-align-items: center;
    -moz-align-items: center;
    align-items: center;
    min-height: 38px;
    padding: 0 25px 0 0;
  }
  .detail-mainNew ul li .wrap .left {
    -webkit-box-flex: 1;
    -webkit-flex: 1;
    -ms-flex: 1;
    flex: 1;
    float: left;
    width: 70%;
    padding: 14px 0 14px 11px;
  }
  .detail-mainNew ul li .wrap .de-btn {
    border-color: #888;
    border: 1px solid #999;
    border-radius: 20px;
    width: 16px;
    height: 16px;
    position: absolute;
    right: 5px;
    top: 50%;
    margin-top: -8px;
  }
  .detail-mainNew ul li.on .de-btn i:after {
    border-width: 0px 1px 1px 0px !important;
    top: 5px !important;
    border-color: #888;
    content: "";
    width: 5px;
    height: 5px;
    position: absolute;
    top: 6px;
    left: 5px;
    border: 1px solid #888;
    border-width: 1px 0px 0px 1px;
    -webkit-transform: rotate(-135deg);
    -ms-transform: rotate(-135deg);
    transform: rotate(-135deg);
  }

  .detail-mainNew  ul li .wrap .left .pic {
    float: left;
    width: 72px;
    height: 72px;
    background-image: url(https://m.elongstatic.com/static/webapp/hotel/2018/10/v15/img/no_pic.png);
    background-repeat: no-repeat;
    position: relative;
    z-index: 1000;
    background-size: 72px 72px;
  }
  .detail-mainNew ul li .wrap .left .pic img {
    width: 72px;
    height: 72px;
  }
  .detail-mainNew ul li .wrap .left .picroom-info {
    margin-left: 83px;
    position: relative;
    z-index: 1000;
    padding-top: 3px;
  }
  .detail-mainNew ul li .wrap .left .room {
    color: #353535;
    font-size: .938rem;
    line-height: .938rem;
  }
  .detail-mainNew ul li .wrap .left .room-info {
    font-size: 12px;
    line-height: 12px;
    margin-top: 8px;
    color: #888;

    overflow: hidden;
    color: #898989;
  }
  .detail-mainNew ul li .info-list {
    background: #FBFBFB;
  }
  .detail-mainNew ul li:first-child {
    border-top: 0;
  }
  .detail-mainNew ul li .info-list ul li {
    border-bottom: 0;
    padding: 8px 64px 8px 12px;
    display: -webkit-flex;
    -webkit-align-items: center;
    align-items: center;
    overflow: hidden;
    position: relative;
    min-height: 85px;
    background: #FBFBFB;
    margin-bottom: 0;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -moz-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -moz-box-align: center;
    -ms-flex-align: center;
    -webkit-box-pack: center;
    -moz-box-pack: center;
    -ms-flex-pack: center;
    -webkit-align-items: center;
    -moz-align-items: center;
    align-items: center;
  }
  .detail-mainNew ul li .info-list ul li:nth-child(1) {
    margin: 0;
    padding: 8px 64px 8px 12px;
  }
  .detail-mainNew ul li .info-list ul li * {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
    -webkit-touch-callout: none;
  }
  .detail-mainNew ul li .info-list ul li .left {
    width: 60%;
  }
  .detail-mainNew ul li .info-list ul li .left div {
    line-height: 1.5rem;
    position: relative;
  }
  .detail-mainNew ul li .info-list ul li .left .bra {
    font-size: .938rem;
  }
  .detail-mainNew  ul li .info-list ul li .left .xstm {
    font-size: .75rem;
    color: #b2b2b2;
  }
  .detail-mainNew ul li .info-list ul li .left .xstm span {
    margin-right: 10px;
  }
  .detail-mainNew ul li .info-list ul li .left .act {
    font-size: 12px;
    line-height: 15px;
    color: #fff;
    margin-top: 0;
    position: relative;
  }
  .detail-mainNew ul li .info-list ul li .value {
    color: #f55;
    text-align: right;
    vertical-align: middle;
    width: 130px;
  }
  .detail-mainNew ul li .info-list ul li * .price {
    font-size: .813rem;
  }
  .detail-mainNew ul li .info-list ul li * .price span {
    font-size: 1.063rem;
  }
  .detail-mainNew ul li .wrap .de-btn i:after {
    border-color: #888;
    content: "";
    width: 5px;
    height: 5px;
    position: absolute;
    top: 3px;
    left: 5px;
    border: 1px solid #888;
    border-width: 1px 0px 0px 1px;
    -webkit-transform: rotate(-135deg);
    -ms-transform: rotate(-135deg);
    transform: rotate(-135deg);
  }
</style>
