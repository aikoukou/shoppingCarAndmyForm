<template>
  <div>
    我的绑定：{{value}}
    <l-form :model="model" :rules="rules">
      <l-form-item label="用户名" prop="username">
        <l-input v-model="model.username"></l-input>
      </l-form-item>
      <l-form-item label="密码" prop="password">
        <l-input v-model="model.password" type="password" value="我是默认值"></l-input>
      </l-form-item>
    </l-form>

    <hr />
    <h3>Element表单</h3>
    <el-form :model="model" :rules="rules" ref="loginForm">
      <el-form-item label="用户名" prop="username">
        <el-input v-model="model.username" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="确认密码" prop="password">
        <el-input type="password" v-model="model.password" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('loginForm')">提交</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
import LInput from "@/components/l-input.vue";
import LFormItem from "@/components/FormItem.vue";
import LForm from "@/components/Form.vue";
export default {
  name: "About",
  provide() { // 跨级通信
    return {
      someval: '来自about'
    }
  },
  components: {
    LInput,
    LFormItem,
    LForm
  },
  data() {
    return {
      value: "",
      model: { username: "", password: "" },
      rules: {
        username: [{ required: true, message: "请输入用户名" },
        {min:3, max:6,message: "最少3位，最多6位"}],
        password: [{ required: true, message: "请输入密码" }]
      }
    };
  },
  methods: {
    submitForm(form) {
      this.$refs[form].validate(valid => {
        if (valid) {
          alert("请求登录!");
        } else {
          alert("校验失败！");
        }
      });
    }
  }
};
</script>

