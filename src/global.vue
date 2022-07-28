// global.vue
<script>
// 全局常量定义
const SignInURL = "/api/login/sign_in";
const SignUpURL = "/api/login/sign_up";

// 全局函数定义
//const testFunc = (message) => console.log(message);

// 全局组件引入
import ajax from 'axios'

export default {
  ajax,
  SignInURL,  // 暴露全局常量
  SignUpURL,
};
</script>