<template>
  <div class="hello">
    <div class="menu">
      <div class="menu-box">
        <div class="menu-left">
          <span></span>
          <span>所有分类</span>
        </div>
        <div class="menu-right">
          <a class="menu-right-m" href="javascript:void(0);">首页</a>
          <a class="menu-right-m" href="javascript:void(0);">今日限时购</a>
          <a class="menu-right-m" href="javascript:void(0);">每日上新</a>
          <a class="menu-right-m" href="javascript:void(0);">国家馆</a>
          <a class="menu-right-m" href="javascript:void(0);">全球旗舰</a>
        </div>
      </div>
    </div>
    <div class="banner">
      <div class="banner-box">
        <div class="banner-menu">
            <div class="leftMenu"  v-for="(item,index) in leftMenu" :key="index" >
              <router-link :to="{ name: '', params: {} }">
                <Icon :type="item.icon"></Icon>
                <span class="t">{{item.name}}</span>
                <Icon type="ios-arrow-right" class="arr"></Icon>
              </router-link>
              <div class="leftMenu-dropRight">
                <div class="dropRight-left" v-for="subNav in item.menuNavs">
                  {{subNav.name}}
                  <!-- <span v-for="nav in item.subNav.subNavs">
                  {{nav.name}}
                  </span> -->
                </div>
                <div class="dropRight-right">

                </div>
              </div>
            </div>
        </div>
      </div>
      <div class="banner-pic">
        <Carousel
        v-model="value2"
        :autoplay="setting.autoplay"
        :autoplay-speed="setting.autoplaySpeed"
        >
            <CarouselItem v-for="(item,index) in files" :key="index">
                <div class="demo-carousel"><img :src="item.img" alt=""></div>
            </CarouselItem>
        </Carousel>
      </div>
    </div>
    <div class="center-info">
      <div class="center-box">
        <div class="left">
          <span><a href="#">100%正品</a></span>
          <span><a href="#">30天无忧退货</a></span>
          <span><a href="#">满88包邮(部分特殊商品除外)</a></span>
        </div>
        <div class="right">
          领考拉1000元新人礼，APP下单更享手机价
        </div>
      </div>
    </div>
    <div class="index-ad">
      <Row :gutter="16">
          <Col span="6" v-for="(item, index) in rowList" :key="index">
              <div><router-link :to="item.url + '=' + item.id"><img :src="item.img" alt=""></router-link></div>
          </Col>
      </Row>
    </div>
    <div class="index-product-a">
      <div class="product-title">
        <h3 class="big">今日限购</h3>
        <span class="product-title-time">
          <div class="top-search-list">
            <ul>
              <li>本场还剩:</li>
            </ul>
          </div>
        </span>
        <p><router-link :to="{ name: '', params: {} }">进入限时购频道></router-link></p>
      </div>
      <div class="product-content">
        <div class="product-content-left">
          <ul>
            <li class="goods" v-for="(item,index) in goodslist">
              <router-link class="goods-left" :to="{ path: '/details', query: {id: item.id} }"><img :src="item.img" alt=""></router-link>
              <div class="goods-right">
                <h3 class="goods-right-title"><router-link :to="{ path: '/details', query: {id: item.id} }">{{item.title}}</router-link></h3>
                <h3 class="goods-right-simple"><router-link :to="{ path: '/details', query: {id: item.id} }">{{item.simple}}</router-link></h3>
                <p class="goods-right-price"><b>¥</b>{{item.price}} <span>¥</span><del>{{item.reprice}}</del></p>
                <div class="goods-right-num"><b></b><p>剩余:{{item.num}}</p></div>
                <span class="goods-right-btn"><router-link :to="{ path: '/product', query: {id: item.id} }">立即抢购</router-link></span>
              </div>
            </li>
          </ul>
        </div>
        <aside class="aside"><router-link :to="buychannel.url"><img :src="buychannel.img" alt=""></router-link></aside>
      </div>
      <div class="clear"></div>
    </div>
    <div class="index-product-a">
      <div class="product-title">
        <h3 class="big">每日上新</h3>
        <span class="product-title-time">
          <div class="top-search-list">
            <ul>
              <li>全世界好物，0点更新</li>
            </ul>
          </div>
        </span>
        <p><router-link :to="{ name: '', params: {} }">进入新货频道></router-link></p>
      </div>
      <div class="product-content-new">
        <div class="product-content-new-left">
          <Row>
              <Col class="goods" span="4" v-for="(item,index) in newGoods" :key="index">
                <router-link class="goodspic" :to="{ path: '/details', query: {id: item.id} }"><img :src="item.img" alt=""></router-link>
                <router-link class="goods-right-title" :to="{ path: '/details', query: {id: item.id} }">{{item.title}}</router-link>
                <p class="goods-right-price"><b>¥</b>{{item.price}} <span>¥</span><del>{{item.reprice}}</del></p>
              </Col>
          </Row>
        </div>
      </div>
      <div class="clear"></div>
    </div>
    <div class="index-brand">
      <h3>热卖品牌：</h3>
      <p v-for="(item, index) in brandList" class="index-brand-link">
        <router-link :to="{ path: '/brand', query: {id: item.id} }"><img :src="item.img" alt=""></router-link>
      </p>
      <div class="clear">
      </div>
    </div>
    <div class="index-product-a">
      <div class="product-title">
        <h3 class="big">美容彩妆</h3>
        <span class="product-title-time">
          <div class="top-search-list">
            <ul>
              <li>热搜词:</li>
              <li v-for="(item, index) in searchList" :key="index"><span>{{item.line}}</span><router-link :to="{ path: '/search', query: {id:item.id} }"><span :class="item.color">{{item.text}}</span></router-link></li>
            </ul>
          </div>
        </span>
        <p><router-link :to="{ name: '', params: {} }">更多好货></router-link></p>
      </div>
      <div class="product-content">
        <div class="product-content-left">
          <ul>
            <li class="goods" v-for="(item,index) in goodslist" :key="index">
              <router-link class="goods-left" :to="{ path: '/details', query: {id: item.id} }"><img :src="item.img" alt=""></router-link>
              <div class="goods-right">
                <h3 class="goods-right-title"><router-link :to="{ path: '/details', query: {id: item.id} }">{{item.title}}</router-link></h3>
                <h3 class="goods-right-simple"><router-link :to="{ path: '/details', query: {id: item.id} }">{{item.simple}}</router-link></h3>
                <p class="goods-right-price"><b>¥</b>{{item.price}} <span>¥</span><del>{{item.reprice}}</del></p>
                <div class="goods-right-num"><b></b><p>剩余:{{item.num}}</p></div>
                <span class="goods-right-btn"><router-link :to="{ path: '/product', query: {id: item.id} }">立即抢购</router-link></span>
              </div>
            </li>
          </ul>
        </div>
        <aside class="aside"><router-link :to="buychannel.url"><img :src="buychannel.img" alt=""></router-link></aside>
      </div>
      <div class="clear"></div>
    </div>
    <show></show>
  </div>
</template>

<script>
import axios from 'axios'
import show from '@/components/downapp'
export default {
  name: 'hello',
  data () {
    return {
      //新品列表
      newGoods: [
        {
          id: 20022,
          img: 'https://haitao.nos.netease.com/98054e290cff4fff84227600f2ec7be61506481743475j82gc0n311429.jpg?imageView&thumbnail=181x0&quality=85',
          title: 'ORIGINS 悦木之源',
          price: '135',
          reprice: '453'
        },
        {
          id: 20023,
          img: 'https://haitao.nos.netease.com/1083c74c205549488d5a387f81fb90ee1507951639605j8qrgzoy13476.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'THERMOS 膳魔师 THV-2001 高真空超轻量不锈钢保温水壶2L 奶油饼干',
          price: '234',
          reprice: '376'
        },
        {
          id: 20024,
          img: 'https://haitao.nos.netease.com/ixtso7c897_800_800.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'NIKE 耐克 AIR MAX KIN 奥利奥跑步鞋 599409-803 女鞋',
          price: '499',
          reprice: '876'
        },
        {
          id: 20025,
          img: 'https://haitao.nos.netease.com/1a07c21f51754b61bf6f295c6b25462d1505286424478j7ioo6mb10655.jpg?imageView&thumbnail=157x0&quality=85',
          title: '【限量秒杀】Apple 苹果 iPhone8(A1863) 64GB 金色 移动联通电信4G手机 国内行货',
          price: '5488',
          reprice: '6800'
        },
        {
          id: 20026,
          img: 'https://haitao.nos.netease.com/1bnq9hn0h5_800_800.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'Vans 范斯 Atwood系列 男款经典低帮休闲板鞋 帆布运动鞋 黑色',
          price: '369',
          reprice: '698'
        },
        {
          id: 20027,
          img: 'https://haitao.nos.netease.com/b2318b559481457bbad3a5833a13a1501507881121375j8plhjkd12521.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'Bruggen 百里香 草莓酸奶水果麦片 500克/袋',
          price: '234',
          reprice: '376'
        },
        {
          id: 20028,
          img: 'https://haitao.nos.netease.com/54eb2b352c014429b84497bed148d3cd1507776235971j8nv1hgv11297.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'AQUTOP 水彩胭脂 10毫升',
          price: '156',
          reprice: '376'
        },
        {
          id: 20029,
          img: 'https://haitao.nos.netease.com/1282c8a701674339a189c60cc5471c781507951713015j8qrikc913481.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'THERMOS 膳魔师 THV-2001高真空超轻量不锈钢保温水壶2L 不锈钢布朗',
          price: '2052',
          reprice: '3706'
        },
        {
          id: 20030,
          img: 'https://haitao.nos.netease.com/89d85288eede46e3a5e901a69014a4351507946687437j8qoiunr13218.jpg?imageView&thumbnail=157x0&quality=85',
          title: '欧舒丹 玫瑰皇后润手霜30毫升*2 乳木果润手霜30毫升*2 牡丹润手霜30毫升',
          price: '234',
          reprice: '376'
        },
        {
          id: 200203,
          img: 'https://haitao.nos.netease.com/156eabbef8f3488bb84a944d1d9722821507519484503j8jm6eoq13644.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'IVANKA TRUMP 伊万卡·特朗普 mara系列女士单肩斜挎包',
          price: '688',
          reprice: '876'
        },
        {
          id: 20022,
          img: 'https://haitao.nos.netease.com/1083c74c205549488d5a387f81fb90ee1507951639605j8qrgzoy13476.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'THERMOS 膳魔师 THV-2001 高真空超轻量不锈钢保温水壶2L 奶油饼干',
          price: '234',
          reprice: '376'
        },
        {
          id: 20022,
          img: 'https://haitao.nos.netease.com/1083c74c205549488d5a387f81fb90ee1507951639605j8qrgzoy13476.jpg?imageView&thumbnail=157x0&quality=85',
          title: 'THERMOS 膳魔师 THV-2001 高真空超轻量不锈钢保温水壶2L 奶油饼干',
          price: '234',
          reprice: '376'
        }
      ],
      searchList: [
        {
          id: 101,
          text: '面膜'
        },
        {
          id: 102,
          line: '|',
          text: 'UGG'
        },
        {
          id: 103,
          line: '|',
          text: '黛安芬'
        },
        {
          id: 104,
          line: '|',
          text: 'sk2'
        },
        {
          id: 105,
          line: '|',
          text: '眼霜'
        },
        {
          id: 106,
          line: '|',
          text: '麦片'
        },
        {
          id: 107,
          line: '|',
          text: '底妆'
        },
        {
          id: 108,
          line: '|',
          text: '水乳'
        },
        {
          id: 109,
          line: '|',
          text: '卸妆',
          color: 'red'
        }
      ],
      //热门品牌
      brandList: [
        {
          id: 100203,
          img: '//haitao.nos.netease.com/ijjnlsle48_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 200203,
          img: '//haitao.nos.netease.com/ihpla8ia63_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 130203,
          img: '//haitao.nos.netease.com/1bmbul3ag44_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 300232,
          img: '//haitao.nos.netease.com/iga62mip96_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 100203,
          img: '//haitao.nos.netease.com/ik7zwsbj78_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 200203,
          img: '//haitao.nos.netease.com/ikz1kjlx68_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 130203,
          img: '//haitao.nos.netease.com/iey592kf19_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        },
        {
          id: 300232,
          img: '//haitao.nos.netease.com/iewkwr7d55_300_300.jpg?imageView&thumbnail=108x0&quality=95'
        }
      ],
      //今日限购列表
      goodslist: [
        {
          id: 100201,
          img: 'https://pop.nosdn.127.net/b06d445b-24ee-4d5f-8ddd-97f51c132e3a?imageView&thumbnail=188x0&quality=85',
          title: '斯凯奇轻质舒适百搭休闲鞋',
          simple: 'Skechers斯凯奇新款时尚轻质休闲鞋 舒适百搭系带鞋女14550',
          price: '105',
          reprice: '262',
          num: 898
        },
        {
          id: 100202,
          img: 'https://pop.nosdn.127.net/755e66df-5e4e-44ec-8526-35c77a8a1a62?imageView&thumbnail=188x0&quality=85',
          title: '小白鞋真皮平底休闲鞋',
          simple: 'keddo2017春夏新品小白鞋真皮女鞋平底休闲鞋女学生鞋子女士单运动鞋',
          price: '269',
          reprice: '596',
          num: 363
        },
        {
          id: 100203,
          img: 'https://pop.nosdn.127.net/08761ce3-2c40-4ae6-b2c1-2b8ac8c3c938?imageView&thumbnail=188x0&quality=85',
          title: '宽松大码显瘦经典帅气',
          simple: 'Herscity 女士外套修身显瘦棒球服飞行员休闲夹克衫',
          price: '159',
          reprice: '596',
          num: 65
        },
        {
          id: 100204,
          img: 'https://haitao.nos.netease.com/it1l480d97_800_800.jpg?imageView&thumbnail=188x0&quality=85',
          title: '澳洲成年人补钙专用',
          simple: '2件装 | 【包税】Devondale 德运 澳洲原产 高钙全脂成人牛奶粉 1000克/袋 2',
          price: '159',
          reprice: '596',
          num: 65
        }
      ],
      buychannel: {
        img: 'https://haitao.nos.netease.com/j0d9lup691_221_378.jpg?imageView&thumbnail=221x378&quality=95',
        url: 'channel'
      },
      dailylimit: [
        {
          id: 10012
        },
        {
          id: 10023
        },
        {
          id: 100233
        },
        {
          id: 20034
        }
      ],
      rowList: [
        {
          id: 2015,
          img: 'https://haitao.nos.netease.com/1bqtv3qm928_265_220.jpg?imageView&thumbnail=265x0&quality=90',
          url: 'active'
        },
        {
          id: 2150,
          img: 'https://haitao.nos.netease.com/1bqtv9chp87_265_220.jpg?imageView&thumbnail=265x0&quality=90',
          url: 'active'
        },
        {
          id: 2563,
          img: 'https://haitao.nos.netease.com/1bqtvah5k1_265_220.jpg?imageView&thumbnail=265x0&quality=90',
          url: 'active'
        },
        {
          id: 3623,
          img: 'https://haitao.nos.netease.com/1bjm6ann672_265_220.jpg?imageView&thumbnail=265x0&quality=90',
          url: 'active'
        }
      ],
      files: [
        {
          id: 1,
          img:'https://haitao.nos.netease.com/DvLD3uNh1HhOGNEKkNxfgffk-ATNpT170100901005_1920_400.jpg?imageView&thumbnail=1920x0&quality=90'
        },
        {
          id: 2,
          img:'https://haitao.nos.netease.com/t1HrtxnD5u62bQfTV94T1709271743_1920_400.jpg'
        },
        {
          id: 3,
          img:'https://haitao.nos.netease.com/uqSDS4ui9t74E4KlPC-8u2ai6T1709271608_1920_400.jpg'
        },
        {
          id: 4,
          img:'https://haitao.nos.netease.com/luEgWGcqvkQTM68h3nIklrT1709291936_1920_400.jpg'
        },
        {
          id: 5,
          img:'https://haitao.nos.netease.com/ZaThSmhAuRXIwoqSfgN0CTXW-N9hQCCA2tLAcsLtzlGzKLi-olfMZlT1709292026_1920_400.jpg'
        }
      ],
      leftMenu: [
        {
          id: 1001,
          icon: 'happy-outline',
          name: '母婴儿童',
          menuNavs: [
            {
              id: 100101,
              name: '奶粉',
              subNavs: [
                {
                  id: 10010101,
                  name: '爱他美'
                },
                {
                  id: 10010102,
                  name: '牛栏'
                },
                {
                  id: 10010103,
                  name: 'Hero Baby'
                },
                {
                  id: 10010104,
                  name: '喜宝'
                },
                {
                  id: 10010105,
                  name: '贝拉米'
                },
                {
                  id: 10010106,
                  name: '美素佳儿'
                },
                {
                  id: 10010107,
                  name: '美林a2'
                },
                {
                  id: 10010108,
                  name: '惠氏'
                }
              ]
            },
            {
              id: 100102,
              name: '纸尿裤/拉拉裤'
            },
            {
              id: 100103,
              name: '营养副食'
            },
            {
              id: 100104,
              name: '宝宝用品'
            },
            {
              id: 100105,
              name: '童装童鞋'
            },
            {
              id: 100106,
              name: '孕妈必备'
            }
          ]
        },
        {
          icon: '',
          name: '美容彩妆'
        },
        {
          icon: '',
          name: '服饰鞋包'
        },
        {
          icon: '',
          name: '家居个护'
        },
        {
          icon: '',
          name: '营养保健'
        },
        {
          icon: '',
          name: '海外直邮'
        },
        {
          icon: '',
          name: '数码家电'
        },
        {
          icon: '',
          name: '环球美食'
        },
        {
          icon: '',
          name: '运动户外'
        },
        {
          icon: '',
          name: '水果生鲜'
        },
        {
          icon: '',
          name: '药品资讯'
        }
      ],
      setting:{
        autoplay: true,
        autoplaySpeed: 5000
      },
      value2: 0
    }
  },
  components: {
    show
  },
  created () {
    //测试axios获取数据
    axios.get('https://m.tuniu.com/mapi/home/getUniqueData').then((res) => {
      console.log(res)
    }).catch((err) => {
      console.log(err);
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello{
  position: relative;
  width: 100%;
  height: 100%;
}
.menu{
  height: 40px;
  background: white;
  width: 100%;
  border-bottom: 2px solid #000;
}
.menu-box{
  max-width: 1080px;
  margin: 0 auto;
  position: relative;
}
.menu-left{
  position: absolute;
  left: 0px;
  background: #000;
  width: 160px;
  height: 40px;
  color: #fff;
  font-size: 14px;
  text-align: center;
  line-height: 40px;
}
.menu-right{
  height: 40px;
  line-height: 40px;
  position: absolute;
  left: 180px;
}
.menu-right a{
  color: #000;
}
.menu-right a:hover{
  color: red;
}
.menu-right-m{
  display: block;
  font-weight: bold;
  font-size: 14px;
  float: left;
  padding-right: 50px;
}
.banner{
  position: relative;
  height: 400px;
  width: 100%;
}
.banner-box{
  position: relative;
  width: 1080px;
  height: 400px;
  margin: 0 auto;
}
.banner-menu{
  position: absolute;
  z-index: 999;
  background: #333;
  opacity: .9;
  left: 50%;
  top: 0;
  margin-left: -540px;
  width: 160px;
  height: 400px;
}
.banner-pic{
  position: absolute;
  width: 100%;
  left: 0;
  top: 0;
  height: 400px;
}
.center-info{
  width: 100%;
  background: white;
  height: 40px;
  border-bottom: 1px solid #eaeaea;
}
.center-box{
  height: 40px;
  line-height: 40px;
  width: 1080px;
  margin: 0 auto;
  position: relative;
}
.center-info .left{
  position: absolute;
  left:0px;
}
.center-info .right{
  position: absolute;
  right:0px;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

// li {
//   display: inline-block;
//   margin: 0 10px;
// }

a {
  color: #42b983;
}
.index-ad{
  width: 1080px;
  margin: 20px auto;
}
.index-product-a{
  width: 1080px;
  margin: 0 auto;
  padding: 20px 0px;
  .product-title{
    width: 100%;
    position: relative;
    height: 60px;
    .big{
      position: absolute;
      left: 0;
      top: 10px;
      font-size: 22px;
      font-weight: bold;
      padding-right: 10px;
    }
    .product-title-time{
      position: absolute;
      left: 100px;
      bottom: 15px;
      color: #666;
      .top-search-list{
        height: 25px;
        line-height: 25px;
      }
      .top-search-list li{
        color: #666;
        float: left;
        padding-right: 5px;
        span{
          padding-right: 5px;
        }
        a{
          color: #666;
        }
        a:hover{
          text-decoration: underline;
        }
      }
    }
    p{
      position: absolute;
      right: 0;
      top: 20px;
      a{
        font-size: 14px;
        color: #333;
      }
      &:hover{
        text-decoration: underline;
      }
    }
  }
  .product-content{
    border-top: 2px solid #000;
    width: 100%;
    .product-content-left{
      ul,li{
        list-style: none;
        margin: 0;
        padding: 0;
      }
      float: left;
      width: 859px;
      border-left: 1px solid #eaeaea;
      .goods{
        position: relative;
        float: left;
        width: 429px;
        height: 189px;
        border-right: 1px solid #eaeaea;
        border-bottom: 1px solid #eaeaea;
        background-color: #fff;
        .goods-left{
          position: relative;
          float: left;
          width: 188px;
          height: 188px;
        }
        .goods-right{
          position: relative;
          float: right;
          width: 230px;
          padding: 0px 15px;
          height: 188px;
          .goods-right-title{
            margin-top: 15px;
            font-size: 14px;
            font-weight: bold;
            width: 100%;
            text-align: left;
            padding: 10px 0px;
            a{
              color: #000;
            }
            &:hover{
              text-decoration: underline;
            }
          }
          .goods-right-simple{
            font-weight: normal;
            font-size: 12px;
            overflow: hidden;
            height: 40px;
            word-break: break-all;
            word-wrap: break-word;
            a{
              color: #666;
            }
            &:hover{
              text-decoration: underline;
            }
          }
          .goods-right-price{
            margin: 14px 0 2px;
            font-size: 24px;
            font-weight: bold;
            color: #e11935;
            span{
              margin-left: 4px;
              font-size: 14px;
              font-weight: normal;
              color: #999;
            }
            del{
              font-size: 14px;
              font-weight: normal;
              color: #999;
            }
          }
        }
        .goods-right-btn{
          position: absolute;
          right: 20px;
          bottom: 20px;
          width: 80px;
          height: 30px;
          background: #de2634;
          color: #fff;
          text-align: center;
          line-height: 30px;
          a{
            color: white;
          }
        }
        .goods-right-num{
          position: relative;
          width: 100px;
          height: 20px;
          line-height: 20px;
          border: 1px solid #f3c7c7;
          border-radius: 10px;
          color: #de2634;
          text-align: left;
          font-size: 12px;
          overflow: hidden;
          b{
            background: #ffd2c5;
            width: 90%;
            height: 100%;
            display: inline-block;
          }
          p{
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            text-align: center;
          }
        }
      }
    }
    .aside{
      float: right;
      width: 221px;
      height: 378px;
    }
  }
  .product-content-new{
    width: 100%;
    .product-content-new-left{
      background: #fff;
      width: 1080px;
      border-left: 1px solid #eaeaea;
      ul,li{
        list-style: none;
        margin: 0;
        padding: 0;
      }
      .goods{
        height: 240px;
        border-right: 1px solid #eaeaea;
        border-bottom: 1px solid #eaeaea;
        background-color: #fff;
        a{
          color: #000;
        }
        a:hover{
          text-decoration: underline;
        }
        img{
          width: 157px;
          height: 157px;
          vertical-align: middle;
          display: inline-block;
        }
        .goodspic{
          display: block;
          margin: 12px;
          width: 157px;
          height: 157px;
        }
        .goods-right-title{
          margin-top: 15px;
          font-size: 12px;
          display: block;
          padding: 0px 10px;
          height: 18px;
          line-height: 18px;
          text-align: center;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }
        .goods-right-price{
          text-align: center;
          font-size: 20px;
          font-weight: bold;
          color: #e11935;
          span{
            margin-left: 4px;
            font-size: 14px;
            font-weight: normal;
            color: #999;
          }
          del{
            font-size: 14px;
            font-weight: normal;
            color: #999;
          }
        }
      }
    }
    .aside{
      float: right;
      width: 221px;
      height: 378px;
    }
  }
}
.leftMenu{
  width: 100%;
  height: 35px;
  line-height: 35px;
  color: white;
  font-size: 14px;
  font-weight: bold;
  text-align: center;
  background: #333;
  .t{
    display: inline-block;
    vertical-align: middle;
    width: 70px;
    height: 30px;
    line-height: 30px;
    white-space: nowrap;
    color: white;
  }
  .arr{
    display: inline-block;
    vertical-align: middle;
    color: #929496;
    font-size: 19px;
    width: 16px;
  }
  &:hover .leftMenu-dropRight{
    display: block;
  }
  .leftMenu-dropRight{
    display: none;
    position: absolute;
    z-index: 9999;
    left: 160px;
    top: 0;
    border: 1px solid #000;
    background: white;
    height: 400px;
    width: 1020px;
    color: black;
  }
}
.dropRight-left{
  float: left;
  width: 70%;
  position: absolute;
  z-index: 9999999;
  color: black;
}
.index-brand{
  margin: 0 auto;
  width: 1080px;
  border: 1px solid #eee;
  background: #fff;
  h3{
    height: 108px;
    line-height: 108px;
    padding: 0px 30px;
    float: left;
  }
  p{
    float: left;
    display: block;
    padding: 0px 5px;
  }
}
.clear{
  clear: both;
}
</style>
