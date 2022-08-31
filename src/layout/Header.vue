<template>
  <div>
    <div>
      <img src="../assets/tech eco.png" style="float: left; max-height: 99px">
    </div>
    <div>
      <el-dropdown>
        <i class="el-icon-setting" style="margin-right: 15px; font-size: xx-large; margin-top: 30px"></i>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>View</el-dropdown-item>
          <el-dropdown-item v-if="!authenticated"><span @click="login">Sign in</span></el-dropdown-item>
          <el-dropdown-item v-else-if="authenticated"><span @click="logout">Sign out</span></el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>

    </div>
  </div>


</template>

<script>
export default {
  name: "Header-page",
  computed:{
    authenticated(){
      return this.$store.getters.authenticated;
    }
  },
  data() {
    return{

    }
  },
  methods:{
    login(){
      this.$router.push('/login')
    },
    logout(){
      localStorage.removeItem("market-token");
      sessionStorage.removeItem("request-url");
      this.$store.commit("logout")
      this.$router.replace('/login')
    }
  }
}
</script>

<style scoped>

</style>