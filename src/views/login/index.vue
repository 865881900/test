<template>
  <div class="login-page">
    <div>
      <div class="login-page_head"> 贵州公共资源交易监管平台</div>
      <div class="login-page_body">
        <!--背景图-->
        <div class="login-page_body-img">
          <div></div>
        </div>
        <!--登录框-->
        <div class="login-page_body-login">
          <div>
            <div class="login-title"><strong>欢迎登陆</strong></div>
            <el-input placeholder="请输入" v-model="username">
              <template slot="prepend">
                <i class="el-icon-user" />
                账号
              </template>
            </el-input>
            <el-input
              placeholder="请输入"
              v-model="password"
              type="password"
              style="margin-bottom: 156px"
              show-password
            >
              <template slot="prepend">
                <i class="el-icon-lock" />
                密码
              </template>
            </el-input>

            <el-button class="login-button" @click="toLogin">登录</el-button>

            <div class="login-link display_flex justify-content_flex-justify">
              <el-button type="text">忘记密码</el-button>
              <el-button type="text">立即注册</el-button>
            </div>
          </div>
        </div>
      </div>
      <div class="login-page_bottom">
        主办：贵州省公共资源交易中心 | 技术支持：广联达科技股份有限公司
        <br />
        CopyRight © 2015 贵州省公共资源交易中心.All Rights Reserved 备案号：黔ICP备14002176号-2
        <br />
        贵公网安备：52010202000320号
      </div>
    </div>
  </div>
</template>

<script>
import { user } from 'api';
import { mapMutations } from 'vuex';

export default {
  name: 'Login',
  data() {
    return {
      password: '',
      username: '',
      verificationCode: ''
    };
  },
  mounted() {
    // this.login();
    // console.log(this.$message.success);
  },
  methods: {
    ...mapMutations('user', ['setIsLogin']),
    // 用户登录
    async toLogin() {
      // 用户登录
      const { code, message } = await user.login();
      if (code === 200) {
        this.$message({
          type: 'success',
          message: '登录成功',
          single: true
        });
        this.$router.replace('/B');
      } else {
        this.$message({
          type: 'warning',
          message: message,
          single: true
        });
      }
    }
  }
};
</script>

<style scoped lang="scss">
input {
  box-shadow: inset 0 0 0 1000px #f7f7f7 !important;
}
.login-page {
  width: 100%;
  height: 100%;
  overflow: auto;
  background: #fff;
  & > div {
    height: 100%;
    min-width: 1000px;
    min-height: 900px;
    .login-page_head {
      width: 100%;
      height: calc((100% - 715px) / 2);
      padding-top: 50.5px;
      padding-left: 60px;
      font-size: 40px;
      font-weight: bold;
      line-height: 36px;
      box-sizing: border-box;
    }
    .login-page_body {
      position: relative;
      display: flex;
      height: 715px;
      padding: 15px 0;
      box-sizing: border-box;
      .login-page_body-img {
        width: 100%;
        height: 685px;
        padding: 21px 0;
        background: #fcfcfc;
        & > div {
          width: 100%;
          height: 100%;
          background: url('../../assets/imgs/login/login-back.png') no-repeat left top;
          background-size: auto 100%;
        }
      }
      .login-page_body-login {
        position: absolute;
        top: 0;
        right: 9.3%;
        display: flex;
        width: 552px;
        height: 100%;
        padding: 0 50px;
        background-color: #fff;
        border-radius: 2px;
        box-shadow: 10px 0 40px 0 rgb(39 100 171 / 20%);
        box-sizing: border-box;
        flex-direction: column;
        align-content: center;
        justify-content: center;
        .login-title {
          margin-bottom: 15px;
          font-size: 32px;
          text-align: center;
          strong {
            position: relative;
            display: inline-block;
            &::after {
              position: absolute;
              top: 48px;
              display: block;
              width: 100%;
              height: 5px;
              background-color: #1e83fe;
              content: '';
            }
          }
        }
        .login-error {
          height: 50px;
          margin-bottom: 10px;
          ::v-deep .el-alert--error.is-light {
            height: 100%;
            line-height: 50px;
            .el-alert__title {
              font-size: 16px;
              color: #ff4b53;
            }
            .el-icon-close {
              top: 19px;
            }
          }
        }
        .login-hint {
          margin-bottom: 52px;
          font-size: 16px;
          line-height: 22px;
          color: #999;
          & > img {
            margin-top: 4px;
          }
          .update_file {
            display: inline-block;
            height: 22px;
            padding: 0;
            line-height: 22px;
          }
        }
        .login-button {
          width: 452px;
          height: 70px;
          margin-bottom: 19px;
          font-size: 24px;
          font-weight: 500;
          line-height: 20px;
          color: #fff;
          background: linear-gradient(142deg, #35a6ff 0%, #197bfd 100%);
          border-radius: 4px;
          box-shadow: 0 8px 15px 0 rgb(15 123 247 / 15%);
        }
        &::after {
          position: absolute;
          top: 0;
          left: -26px;
          display: block;
          width: 0;
          height: 0;
          border-top: 18px solid transparent;
          border-right: 13px solid #0c53a8;
          border-bottom: 18px solid #0c53a8;
          border-left: 13px solid transparent;
          content: '';
        }
        & i {
          color: #999;
        }
      }
    }
    .login-page_bottom {
      display: flex;
      width: 100%;
      height: calc((100% - 715px) / 2);
      font-size: 14px;
      line-height: 25px;
      text-align: center;
      box-sizing: border-box;
      flex-direction: column;
      justify-content: center;
    }
  }
}
.login-icon {
  display: inline-block;
  width: 14px;
  height: 14px;
  margin-right: 10px;
}
.el-button {
  font-size: 16px;
  color: #1e83fe;
  :hover {
    text-decoration: underline;
  }
}
.el-input-group {
  height: 43px;
  margin-bottom: 20px;
  border-top: none;
  border-right: none;
  border-left: none;
  ::v-deep .el-input-group__prepend {
    width: 80px;
    padding: 0 20px 0 0;
    font-size: 16px;
    color: #333;
    box-sizing: border-box;
  }
  & > ::v-deep .el-input__inner {
    height: 43px;
    line-height: 43px;
    background: none !important;
  }
}
</style>
