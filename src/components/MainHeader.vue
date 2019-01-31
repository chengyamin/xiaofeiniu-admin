<template>
  <div class="xfn-main-header">
    <h3 class="xfn-title">{{$store.state.globalSettings.appName}}后台管理</h3>
    <div class="xfn-right">
    当前用户：{{$store.state.adminName}}
    <el-button >退出</el-button>
    </div>
  </div>
</template>

<script>
export default{
  methods:{
    quit(){
      //清除当前用户的登录信息
      this.$store.commit('setAdminName','');
      //跳转回登录页
      this.router.push('./login');
    }
  },
  mounted(){
    //将$store存储的全局配置数据赋值给中间变量-formData,方便表单元素执行双向数据绑定
    this.formData=this.$store.state.globalSettings;
  }
}
</script>

<style lang="scss">
$header-height:60px;
.xfn-main-header{
  background:#DCDFE6;
  border-radius:4px;
  line-height:$header-height;
  height:$header-height;
  padding:0 6px;

  .xfn-title{
    color:#303133;
    float:left;
    margin:0;
  }
  .xfn-right{
    float:right;

  }
}
</style>