<template>
  <div class="login">
    <el-form
      class="form_content"
      :model="loginForm"
      status-icon
      :rules="rules"
      ref="loginForm"
      label-width="100px"
      label-position="right"
    >
      <el-form-item label="用户名" prop="userName">
        <el-input
          type="text"
          v-model="loginForm.userName"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input
          type="password"
          v-model="loginForm.password"
          autocomplete="off"
        ></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('loginForm')"
          >登录</el-button
        >
        <el-button @click="resetForm('loginForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    var validateUserName = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入用户名"));
      } else if (value !== "admin") {
        callback(new Error("用户名验证错误"));
      } else {
        callback();
      }
    };
    var validatePassword = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else if (value !== "123") {
        callback(new Error("密码验证错误"));
      } else {
        callback();
      }
    };
    return {
      rules: {
        userName: [
          { validator: validateUserName, required: true, trigger: "blur" },
        ],
        password: [
          { validator: validatePassword, required: true, trigger: "blur" },
        ],
      },
      loginForm: {
        userName: "",
        password: "",
      },
    };
  },
  methods: {
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$message({
            message: "登录成功",
            type: "success",
          });
          this.$router.push("/about");
        } else {
          return false;
        }
      });
    },
  },
};
</script>
<style scoped>
.form_content{
  width:60%;
  margin: auto;
}
.login{
  height: 100%;
  text-align: center;
}
</style>
