<template>
  <div>
    <h1>REGISTRATION</h1>
    <br>
    <el-row>
      <el-col :span="12" :offset="6">
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="120px" class="demo-ruleForm">
          <el-form-item label="Name" prop="name">
            <el-input placeholder="Please input your name" v-model="ruleForm.name"></el-input>
          </el-form-item>
          <el-form-item label="LastName" prop="lastName">
            <el-input placeholder="Please input your Surname" v-model="ruleForm.lastName"></el-input>
          </el-form-item>
          <el-form-item label="Login" prop="login">
            <el-input placeholder="Please input a login" v-model="ruleForm.login"></el-input>
          </el-form-item>
          <el-form-item label="Password" prop="password">
            <el-input placeholder="Please input password" v-model="ruleForm.password" show-password></el-input>
          </el-form-item>
          <el-form-item label="Email" prop="email">
            <el-input placeholder="Please input your email" v-model="ruleForm.email"></el-input>
          </el-form-item>
          <el-form-item label="Date of Birth" prop="dateOfBirth">
            <el-date-picker type="date" placeholder="Please input your date fo birth" v-model="ruleForm.dateOfBirth" style="width: 100%;"></el-date-picker>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">Submit</el-button>
            <el-button @click="resetForm('ruleForm')">Reset</el-button>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>

  </div>
</template>

<script>
import axios from "axios";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Registration",
  data() {
    return {
      ruleForm: {
        name: '',
        lastName: '',
        type: [],
        password: '',
        login: '',
        email: '',
        dateOfBirth: '',
        roles: [
          {name: "ROLE_USER"}
        ]
      },
      rules: {
        name: [
          { required: true, message: 'Please input Name', trigger: 'blur' },
          { min: 3, max: 25, message: 'Length should be 3 to 25', trigger: 'blur' }
        ],
        lastName: [
          { required: true, message: 'Please input Surname', trigger: 'blur' },
          { min: 3, max: 25, message: 'Length should be 3 to 25', trigger: 'blur' }
        ],
        email: [
          {required: true, message: 'Please input email', trigger: 'blur'},
          {email: true, message: 'Please, input correct email', trigger: 'blur'}
        ],

        type: [
          { type: 'array', required: true, message: 'Please select at least one activity type', trigger: 'change' }
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          axios.post("api/register", this.ruleForm)
              .then(res=>{
                console.log(res)
                this.ruleForm = {};
                alert('Registered successfully !!!');
                this.$router.push("/login")
              })
        } else {
          console.log('error submit!!');
          return false;
        }
      });

    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style scoped>
  .el-form-item {
    width: 700px;
  }
</style>