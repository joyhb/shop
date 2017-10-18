<template>
  <div class="header-top">
    <div class="header">
      <div class="header-menu">
        <span class="name">考拉欢迎你!</span>
        <span class="login"><a href="javascript:void(0);">登录</a> &nbsp;|&nbsp; <a href="javascript:void(0);">免费注册</a></span>
        <span class="mobile"><img src="../assets/images/mobile.png" alt=""></span>
        <span class="app"><a href="javascript:void(0);" @mouseover="toggleShow()" @mouseout="toggleShow()">手机考拉海购</a></span>
        <span class="showcode" v-show="isShow"></span>
        <span class="other">
          <a class="other-menu" href="javascript:void(0);">每日签到</a>
          <i class="other-menu">|</i>
          <a class="other-menu" href="javascript:void(0);">我的订单</a>
          <i class="other-menu">|</i>
          <span class="other-menu">
            <Dropdown>
                <a href="javascript:void(0)">
                    个人中心
                    <Icon type="arrow-down-b"></Icon>
                </a>
                <DropdownMenu slot="list">
                    <DropdownItem>我的优惠券</DropdownItem>
                    <DropdownItem>我的考拉豆</DropdownItem>
                    <DropdownItem>账号管理</DropdownItem>
                    <DropdownItem>我的实名认证</DropdownItem>
                    <DropdownItem>北京烤鸭</DropdownItem>
                    <DropdownItem>我的收藏商品</DropdownItem>
                    <DropdownItem>我的关注商品</DropdownItem>
                </DropdownMenu>
            </Dropdown>
          </span>
          <i class="other-menu">|</i>
          <span class="other-menu">
            <Dropdown>
                <a href="javascript:void(0)">
                    客户服务
                    <Icon type="arrow-down-b"></Icon>
                </a>
                <DropdownMenu slot="list">
                    <DropdownItem>联系客服</DropdownItem>
                    <DropdownItem>帮助中心</DropdownItem>
                </DropdownMenu>
            </Dropdown>
          </span>
          <i class="other-menu">|</i>
          <span class="other-menu">
            <Dropdown>
                <a href="javascript:void(0)">
                    充值中心
                    <Icon type="arrow-down-b"></Icon>
                </a>
                <DropdownMenu slot="list">
                    <DropdownItem>话费流量</DropdownItem>
                    <DropdownItem>游戏充值</DropdownItem>
                </DropdownMenu>
            </Dropdown>
          </span>
          <i class="other-menu">|</i>
          <a class="other-menu" href="javascript:void(0);">消费者告知书</a>
          <i class="other-menu">|</i>
          <a class="other-menu" href="javascript:void(0);">更多</a>
        </span>
      </div>
    </div>
    <div class="top" id="top" :class="searchBarFixed == true ? 'topFixed': ''">
      <div class="top-content">
        <a href="/" class="top-content-logo"></a>
        <div class="top-search">
          <div class="top-search-box">
            <div class="top-search-input">
              <input class="search-input" v-model="searchKeyWord" type="text" name="" value="searchKeyWord">
            </div>
            <router-link :to="'/search?query=' + searchKeyWord">
              <span class="top-search-icon"><Icon type="ios-search-strong"></Icon></span>
            </router-link>
          </div>
          <div class="top-search-list">
            <ul>
              <li v-for="(item, index) in searchList" :key="index"><span>{{item.line}}</span><router-link :to="{ path: '/search', query: {id:item.id} }"><span :class="item.color">{{item.text}}</span></router-link></li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      searchBarFixed: false,
      searchKeyWord: 'agatha项链',
      isShow: false,
      searchList: [
        {
          id: 101,
          text: '面膜'
        },
        {
          id: 102,
          line: '|',
          text: '德运'
        },
        {
          id: 103,
          line: '|',
          text: '铁元'
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
          text: '电动牙刷'
        },
        {
          id: 108,
          line: '|',
          text: '乳胶枕'
        },
        {
          id: 109,
          line: '|',
          text: '话费充值',
          color: 'red'
        }
      ]
    }
  },
  methods: {
    handleScroll () {
      let scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop
      let offsetTop = document.querySelector('#top').offsetTop
      if (scrollTop > offsetTop) {
        this.searchBarFixed = true
      } else {
        this.searchBarFixed = false
      }
    },
    toggleShow: function () {
      this.isShow = !this.isShow
    }
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  },
}
</script>

<style lang="scss" scoped>
.top{
  height: 100px;
  width: 100%;
  background: white;
  .top-content{
    max-width: 1080px;
    margin: 0 auto;
    position: relative;
    .top-content-logo{
      position: absolute;
      left: 0;
      top: 29px;
      width: 220px;
      height: 42px;
      line-height: 45px;
      outline: none;
      cursor: pointer;
      z-index: 9;
      background: url(http://haitao.nos.netease.com/264271ddbec447288f17aef71119b1f4.png) no-repeat;
    }
  }
}
.topFixed{
  position: fixed;
  top: 0;
  z-index: 99999999;
  box-shadow: 0 0px 10px rgba(0,0,0,0.2);
}
.listNone{
  display: none;
}
.top-search{
  position: absolute;
  top: 24px;
  left: 343px;
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
  .top-search-box{
    width: 510px;
    height: 36px;
    padding-left: 1px;
    background-color: #333;
    .top-search-input{
      float: left;
      margin: 2px 1px;
      padding: 4px 5px 4px 30px;
      background-color: #fff;
      white-space: normal;
      word-wrap: break-word;
    }
    .search-input{
      width: 423px;
      height: 24px;
      line-height: 24px;
      border: 0;
      font-size: 13px;
    }
    .top-search-icon{
      display: inline-block;
      height: 36px;
      width: 48px;
      font-size: 25px;
      line-height: 36px;
      color: #fff;
      text-align: center;
      cursor: pointer;
      float: left;
    }
  }
}
.header{
  background: #eee;
  width: 100%;
  height: 30px;
  font-size: 12px;
  color: #666;
}
.header-menu{
  position: relative;
  max-width: 1080px;
  margin: 0 auto;
  height: 30px;
  line-height: 30px;
}
.login{
  white-space: nowrap;
  position: absolute;
  left: 90px;
}
.login a{
  color: #666;
}
.login a:hover{
  color: red;
}
.mobile{
  width: 16px;
  height: 16px;
  position: absolute;
  top: 3px;
  left: 210px;
}
.app{
  position: absolute;
  left: 230px;
}
.showcode{
  width: 116px;
  height: 116px;
  background: white;
  position: absolute;
  z-index: 999999;
  top: 30px;
  left: 200px;
  background-image: url(../assets/images/code.jpg);
}
.app a{
  color: #666;
}
.app a:hover{
  color: red;
}
.other{
  color: #666;
  position: absolute;
  right: 0px;
}
.other-menu{
  display: block;
  padding: 0px 10px;
  /*width: 80px;*/
  float: left;
}
.other a{
  color: #666;
}
.other a:hover{
  color: red;
}
.red{
  color: red;
}
</style>
