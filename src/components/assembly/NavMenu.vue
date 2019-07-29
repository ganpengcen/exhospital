<template>
  <el-aside style="width: 256px;">
    <el-menu :default-active="activeIndex" text-color="#909191" active-text-color="#834295" class="el-menu-vertical-demo" :collapse="this.$store.state.isCollapse" :unique-opened="true" @select="handleSelect">
      <el-submenu index="1">
        <template slot="title" class="el-icon1"><i class="el-icon-mobile-phone"></i><span>Dashboard</span></template>
        <el-menu-item index="/Page">监控台</el-menu-item>
      </el-submenu>
      <el-submenu index="2">
        <template class="el-icon1" slot="title"><i class="el-icon-menu"></i><span>系统管理</span></template>
        <el-menu-item index="/index2">操作日志</el-menu-item>
        <el-menu-item index="">操作员</el-menu-item>
      </el-submenu>
      <el-submenu index="3">
        <template slot="title"><i class="el-icon-setting"></i><span>基础设置</span></template>
        <el-menu-item index="">词典</el-menu-item>
        <el-menu-item index="">自定义项</el-menu-item>
        <el-menu-item index="">医生</el-menu-item>
      </el-submenu>
      <el-submenu index="4">
        <template slot="title"><i class="el-icon-time"></i><span>会员管理</span></template>
        <el-menu-item index="">会员注册</el-menu-item>
        <el-menu-item index="">个人档案</el-menu-item>
        <el-menu-item index="">充值管理</el-menu-item>
        <el-menu-item index="">订单管理</el-menu-item>
      </el-submenu>
      <el-submenu index="5">
        <template slot="title"><i class="el-icon-star-on"></i><span>会员积分</span></template>
        <el-menu-item index="">积分兑换</el-menu-item>
        <el-menu-item index="">积分规则</el-menu-item>
        <el-menu-item index="">兑换规则</el-menu-item>
        <el-menu-item index="">积分调整</el-menu-item>
      </el-submenu>
      <el-submenu index="6">
        <template slot="title"><i class="el-icon-time"></i><span>产品管理</span></template>
        <el-menu-item index="">产品列表</el-menu-item>
        <el-menu-item index="">预约管理</el-menu-item>
        <el-menu-item index="">处理结果</el-menu-item>
      </el-submenu>
      <el-submenu index="7">
        <template slot="title"><i class="el-icon-tickets"></i><span>报表管理</span></template>
        <el-menu-item index="">我的报表</el-menu-item>
      </el-submenu>
    </el-menu>
  </el-aside>
</template>

<script>
    export default {
        name: "NavMenu",
      data() {
        return {
          name: '',
          path: '',
          flag: 0,
        }
      },
      computed: {
        activeIndex() {
          return this.$route.path
        }
      },
      mounted() {
        /*动态标签页切换功能开始
        * 实现多页面查看
        * 类似浏览器功能
        *
        * */
        var menu = document.getElementsByClassName('el-menu')[0];
        var _this = this;
        menu.addEventListener('click', function(e) {
          // setTimeout(() => {
          var ev = e.target || e.srcElement;
          console.log(ev.tagName);
          if(ev.tagName.toLowerCase() != 'li') {
            return false;
          }
          _this.$store.commit('changeCheckMenu', true);
          _this.name = ev.innerHTML;
            var tags = _this.$store.state.tags;
          if(tags.length > 0) {
            for(var i = 0; i<tags.length; i++) {
              //console.log(tags[i].name, _this.name)
              if(tags[i].name == _this.name) {
                _this.flag = 1;
                break;
              }else {
                _this.flag = 0;
              }
            }
          }else {
            _this.flag = 0;
          }
          if(_this.flag == 0) {
            console.log("path", _this.path)
            _this.$store.commit('addTags', { name: _this.name, currentPath: _this.path, type: '', active: true });
          }
          console.log('sss')
          _this.$router.push({ path: _this.path })
          // },300);
          //console.log(_this.$store.state.tags)
        })

        /*
        * 动态标签页切换功能结束
        * */
      },
      watch: {
        '$route'(to, from) {
          // console.log("to", to.path);
          this.path = to.path;
          this.$store.commit('changeActive', to.path)
        }
      },
      methods: {
        handleClose(val) {
          //console.log(val)
        },
        handleSelect(key, path) {
          console.log("select:", key, path);
          this.path = key;

        }
      }
    }
</script>

<style scoped>
  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 256px;
  }
  .el-menu {
    padding-top: 60px;
    min-height: 100%;
  }
  .el-aside {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    z-index: 2;
  }
  a {
    display: block;
    width: 100%;
    height: 100%;
    text-decoration: none;
    color: #909191;
  }
  .el-aside ul {
    box-sizing: border-box;
  }
  .el-menu-item.is-active {
    border-left:#834295 4px solid ;
    background-color: rgba(131, 66, 149, 0.2) !important;
  }
  .el-menu-item:hover {
    border-left:#834295 4px solid ;
    background-color: rgba(131, 66, 149, 0.2) !important;
  }
  .el-menu--horizontal>.el-menu-item:hover:hover{
    border-left:#834295 4px solid ;
    background-color: rgba(131, 66, 149, 0.2) !important;
  }

</style>
