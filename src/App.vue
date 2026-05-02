<template>
  <div class="login-container">
    <div class="login-card">
      <div class="logo-area">
        <div class="logo-circle">📚</div>
      </div>
      
      <div class="system-title">📖 学生成绩管理系统</div>
      <div class="sub-welcome">登录后管理成绩 · 掌握学习动态</div>

      <div class="input-group">
        <div class="input-label">📧 电子邮箱 / 用户名</div>
        <input 
          type="text" 
          class="input-field" 
          v-model="username"
          placeholder="teacher@school.com 或 你的工号"
          @keypress.enter="handleLogin"
        >
      </div>

      <div class="input-group">
        <div class="input-label">🔒 密码</div>
        <input 
          type="password" 
          class="input-field" 
          v-model="password"
          placeholder="········"
          @keypress.enter="handleLogin"
        >
      </div>

      <div class="options">
        <label class="remember">
          <input type="checkbox" v-model="rememberMe"> 记住我
        </label>
        <a href="#" class="forgot" @click.prevent="forgotPassword">忘记密码？</a>
      </div>

      <button class="login-btn" @click="handleLogin">登 入 系 统 →</button>

      <div class="signup-prompt">
        还没有教师账号？
        <a href="#" class="signup-link" @click.prevent="contactAdmin">联系管理员</a>
      </div>
      
      <div class="demo-hint">
        💡 演示账号：任意输入，点击登录即可
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      username: '',
      password: '',
      rememberMe: false
    }
  },
  mounted() {
    const savedUser = localStorage.getItem('savedUsername');
    if (savedUser) {
      this.username = savedUser;
      this.rememberMe = true;
    }
  },
  methods: {
    handleLogin() {
      if (!this.username.trim()) {
        alert('👀 请输入账号');
        return;
      }
      if (!this.password.trim()) {
        alert('🔐 请输入密码');
        return;
      }

      if (this.rememberMe) {
        localStorage.setItem('savedUsername', this.username);
      } else {
        localStorage.removeItem('savedUsername');
      }

      localStorage.setItem('currentUser', this.username);
      
      alert(`✅ 欢迎 ${this.username}\n进入「学生成绩管理系统」`);
    },
    forgotPassword() {
      alert('📧 请联系管理员重置密码：admin@school.com');
    },
    contactAdmin() {
      alert('👩‍🏫 请联系教务处申请账号');
    }
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.login-container {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 20px;
  background: linear-gradient(145deg, #0f172a 0%, #1e1b4b 100%);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
}

.login-card {
  background: rgba(255, 255, 255, 0.96);
  backdrop-filter: blur(2px);
  border-radius: 48px;
  padding: 48px 40px;
  width: 100%;
  max-width: 440px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
}

.logo-area {
  text-align: center;
  margin-bottom: 28px;
}

.logo-circle {
  background: linear-gradient(135deg, #667eea, #764ba2);
  width: 70px;
  height: 70px;
  border-radius: 35px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
  box-shadow: 0 12px 20px -8px rgba(102, 126, 234, 0.4);
}

.system-title {
  text-align: center;
  font-size: 22px;
  font-weight: 700;
  background: linear-gradient(135deg, #1e293b, #334155);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin-bottom: 8px;
}

.sub-welcome {
  text-align: center;
  color: #64748b;
  font-size: 13px;
  margin-bottom: 32px;
}

.input-group {
  margin-bottom: 24px;
}

.input-label {
  display: block;
  font-size: 13px;
  font-weight: 600;
  color: #334155;
  margin-bottom: 8px;
}

.input-field {
  width: 100%;
  padding: 16px 18px;
  font-size: 15px;
  border: 2px solid #e2e8f0;
  border-radius: 28px;
  background: white;
  transition: all 0.2s;
  outline: none;
}

.input-field:focus {
  border-color: #8b5cf6;
  box-shadow: 0 0 0 4px rgba(139, 92, 246, 0.15);
}

.options {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 28px;
  font-size: 13px;
}

.remember {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #475569;
  cursor: pointer;
}

.forgot {
  color: #8b5cf6;
  text-decoration: none;
  font-weight: 500;
}

.forgot:hover {
  text-decoration: underline;
}

.login-btn {
  width: 100%;
  background: linear-gradient(100deg, #667eea, #764ba2);
  border: none;
  padding: 16px;
  border-radius: 40px;
  color: white;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.25s;
  box-shadow: 0 8px 20px rgba(102, 126, 234, 0.3);
  margin-bottom: 24px;
}

.login-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 15px 28px -8px rgba(102, 126, 234, 0.5);
}

.login-btn:active {
  transform: translateY(1px);
}

.signup-prompt {
  text-align: center;
  font-size: 14px;
  color: #5b6e8c;
  border-top: 1px solid #edf2f7;
  padding-top: 24px;
}

.signup-link {
  color: #8b5cf6;
  font-weight: 700;
  text-decoration: none;
  margin-left: 6px;
}

.demo-hint {
  text-align: center;
  font-size: 12px;
  color: #94a3b8;
  margin-top: 18px;
  background: #f8fafc;
  padding: 8px 12px;
  border-radius: 40px;
  display: inline-block;
  width: 100%;
}
</style>