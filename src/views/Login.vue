<template>
  <div class="login">
    <el-card class="xfn-login-card">
      <div slot="header">管理员登录</div>
      <div>
        <el-form label-width="100px">
          <el-form-item label="管理员名：">
            <el-input v-model="fromData.aname" placeholder="请输入管理员名"></el-input>
          </el-form-item>

          <el-form-item label="登录密码：">
            <el-input type="password" v-model="fromData.apwd" placeholder="请输入管理员密码"></el-input>
          </el-form-item>

          <el-form-item>
            <el-button type="primary" @click.native="doLogin">登录</el-button>
            <el-button @click="doCancel">取消</el-button>
          </el-form-item>  
        </el-form>
      </div>
    </el-card>
    {{$store.state.globalSettings}}
  </div>
</template>
<script>
export default {
  data(){//普通组件
    return {
      fromData:{//表单中用户输入的两个数据
        aname:'admin',
        apwd:'123456'
      }
    }
  },
  methods:{
    doLogin(){//执行登录
      var url=this.$store.state.globalSettings.apiUrl+`/admin/login/${this.fromData.aname}/${this.fromData.apwd}`;
      // console.log(url);
      this.$axios.get(url).then((res)=>{
        // console.log(res.data);
        if(res.data.code==200){//登陆成功
        //把用户名存入Vuex存储仓库
        this.$store.commit('setAdminName',this.fromData.aname);
          this.$router.push('/main');
        }else{//登录失败
          this.$alert('用户名或者密码有误！','登录失败',{type:'error'});
        }
      }).catch((err)=>{
        console.log(err)
        })
    },
    doCancel(){//清除用户的输入
      this.formData.aname='';
      this.formData.apwd='';
    }
  }
}
</script>
<style lang="scss">
  .xfn-login-card{
    width:450px;
    margin:150px auto;
    .el-card__header{
      text-align:center;
      font-size:1.2em;
    }
  }

</style>

