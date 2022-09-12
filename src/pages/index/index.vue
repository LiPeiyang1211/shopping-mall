<template>
  <div class='home'>
    <div class="header">
      <h1 class="zhaohe">兆和</h1>
    </div>
    <div class="official"></div>
    <div class="swiper">
        <mt-swipe :auto="4000">
            <mt-swipe-item >
                <img src="https://lipeiyang-test-1311381084.cos.ap-nanjing.myqcloud.com/%E5%85%86%E5%92%8C%E5%95%86%E5%9F%8E%2F%E7%B1%B3%E9%9D%A2%E7%B2%AE%E6%B2%B9%2F20220906_102724_0000.png">
            </mt-swipe-item>
        </mt-swipe>
    </div>
    <div class="icon">
        <ul class='icon-ul'>
            <li class='icon-li' v-for="(list,index) in routers" :key='index'>
              <router-link :to="{ path: list.src }" >
                <div  class="wenzi">
                <img :src="list.img" alt="Zaohe">
                
                  <p class="shopname">{{list.shopname}}</p>
                </div>
              </router-link>
            </li>
        </ul>
    </div>
    <div class="main">
        <div class="main-box" v-for="(list,index) in shopListData" :key="index">
            <h2>{{list.title}}</h2>
            <ul>
                <li v-for="(v,i) in list.data" :key='i' @click="jumpDetail(list,v)">
                    <div class="list">
                        <div class="image">
                            <img :src="v.img_url" alt="图片">
                            
                        </div>
                        <p class="name">{{v.name}}</p>
                        <p class="nametwo">{{v.content}}</p>
                        <p class="price">￥ {{toFixed(v.price)}} </p>
                    </div>
                </li>
            </ul>  
        </div>
    </div>
    <v-footer></v-footer>
  </div>
</template>
<script>
import { getData } from '@/api/data'
import footer from "@/components/footer/index";
export default {
  name: "index",
  data() {
    return {
      routers: [
        {
          img: "/static/img/xuangou.jpg",
          src: "/phone",
          shopname:"选购糕点"
        },
        {
          img: "/static/img/peijian.jpg",
          src: "/parts",
          shopname:"粮油调味"
        },
        {
          img: "/static/img/pingbao.jpg",
          src: "/",
          shopname:"联系客服"
        },
        {
          img: "/static/img/dingzhi.jpg",
          src: "/",
          shopname:"定制礼盒"
        }
      ],
      shopListData: []
    };
  },
  methods: {
    jumpDetail(list,v) {
     

      this.$router.push({
        path: "detail",
        query: {
          id: v.id,
          shop_id: list.id
        }
      });
    },
    toFixed(value) {
      return JSON.parse(value).toFixed(2)
    },
    homeShopListData() {
      getData().then(res=> {
        this.shopListData = res.homeData;
      })
    },
  },
  mounted() {
    this.homeShopListData();
  },
  components: {
    "v-footer": footer
  },
};
</script>

<style lang="less" scoped>
  .home {
    width: 100%;
    height: auto;
    .header {
      position: fixed;
      width: 100%;
      top: 0;
      z-index: 1;
      height: 1.45rem;
      line-height: 1.45rem;
      font-size: 0.35rem;
      background: black;
      h1 {
        font-size: 0.55rem;
        color: #EFEFF2;
        text-align: center;
        display: block;
      }
    }
    .official {
      width: 100%;
      height: 0.8rem;
      background: white;
      margin-top: 1.45rem;
      background: url("/static/img/official.png") no-repeat;
      background-size: 100% 100%;
    }
    .swiper {
      margin-top: 1px;
      height: 5.3rem;
      img {
        width: 100%;
        height: 5.3rem;
      }
    }
    .icon {
      width: 100%;
      height: 2rem;
      background: white;
      border-bottom: 1px solid #f4f4f4;
      .icon-ul {
        width: 100%;
        height: 100%;
        .icon-li {
          width: 25%;
          height: 100%;
          float: left;
          margin: auto;
          a {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            
            img {
              display: block;
              width: 70%;
            }
            .wenzi{
              
              display:flex;
              justify-content: center;
              align-items: center;
              flex-direction:column;
              p{
                font-size: 0.29rem;
              }
            }
          }
        }
      }
    }
    .main {
      margin-bottom: 1.6rem;
      h2 {
        display: block;
        height: 1.6rem;
        background: #f7f7f7;
        font-size: 0.49rem;
        line-height: 1.6rem;
        color: #333;
        text-align: center;
      }
      h2::before,
      h2::after {
        position: relative;
        margin: 0 0.12rem;
        display: inline-block;
        content: " ";
        height: 1px;
        width: 0.4rem;
        background-color: #9c9c9c;
        top: -0.16rem;
      }
      ul {
        width: 100%;
        height: auto;
        overflow: hidden;
      }
      li {
        list-style: none;
        .list {
          width: 50%;
          height: auto;
          background: white;
          float: left;
          border-right: 1px solid #f4f4f4;
          border-top: 1px solid #f4f4f4;
          padding-bottom: 0.25rem;
          .price {
            margin: auto;
            text-align: center;
            font-size: 0.38rem;
            color: #f81200;
            font-weight: 500;
            padding-top: 0.8rem;
            padding-bottom: 0.2rem;
          }
          .name {
            width: 80%;
            height: 0.64rem;
            line-height: 0.5rem;
            overflow: hidden;
            white-space: nowrap;
            text-overflow: ellipsis;
            margin: auto;
            font-size: 0.38rem;
            font-weight: 800;
            text-align: center;
          }
          .nametwo {
            width: 90%;
            font-size: 0.29rem;
            text-align: center;
            overflow: hidden;
            margin: auto;
            display: -webkit-box;
            -webkit-box-orient: vertical;
            -webkit-line-clamp: 2;
          }
          .image {
            width: 100%;
            background: white;
            padding-top: 0.2rem;
            padding-bottom: 0.3rem;
            img {
              width: 2.48rem;
              height: 2.6rem;
              display: block;
              margin: auto;
              margin-top: 0.4rem;
              margin-bottom: 0.2rem;
            }
          }
        }
      }
    }
  }
</style>
