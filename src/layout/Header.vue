<template>
  <div>
    <el-dropdown>
      <i class="el-icon-setting" style="margin-right: 15px"></i>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item>View</el-dropdown-item>
        <el-dropdown-item v-if="!authenticated"><span @click="login">Sign in</span></el-dropdown-item>
        <el-dropdown-item v-else-if="authenticated"><span @click="logout">Sign out</span></el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
    <span style="font-weight: bold; font-size: x-large; color: #114fbe">{{fullName}}</span>
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
      fullName: this.$store.getters.account.name + " " + this.$store.getters.account.lastName
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