<template>
  <div class="hello">
    <div class="logo">
      <img src="@/assets/logo.png">
    </div>
    <ul>
      <li><router-link to="/" style="color: #85cb6c;">TRANG CHỦ</router-link></li>
      <li><router-link to="/doctorteam" style="color: #54595f;">ĐỘI NGŨ Y BÁC SĨ</router-link></li>
      <li><router-link to="/myservice" style="color: #54595f;">DỊCH VỤ</router-link></li>
      <li v-if="!isLogin"><router-link to="/login" style="color: #54595f;">ĐĂNG NHẬP</router-link></li>
      <li v-else>
        <span><router-link to="/history">Xin chào, {{ name }}</router-link></span>
        <button @click="logout()" style="width: 120px; height: 40px" class="logoutbutton">ĐĂNG XUẤT</button>
      </li>
    </ul>  
    <button style="width: 120px; height: 40px; margin-left: 20px;"><router-link to="/booking">
        <p>ĐẶT LỊCH</p>
      </router-link></button>
  </div>
</template>

<script>

export default {
  data() {
    return {
      isLogin: false,
      name: null
    }
  },
  methods: {
    logout() {
      localStorage.clear();
      this.isLogin = false;
      window.location.reload();
    }
  },

  mounted() 
  {
    console.log(window.localStorage)
    const logstate = window.localStorage.getItem('isLogedin');
    const username = window.localStorage.getItem('username');
    this.isLogin = logstate;
    this.name = username
    console.log(this.isLogin);
    console.log(logstate);
    console.log(this.name);
  }
}


</script>

<style>
.hello {
  display: flex;
  text-decoration: none;
  display: flex;
  color: #1e4d7c;
  margin-top: 10px;
  height: 70px;
}

.logo img {
  margin-left: 270%;
  flex: 0;
  width: 70px;
  height: auto;
}

ul {
  margin-left: 30%;
  list-style-type: none;
  padding: 0;
}

li {
  font-weight: bold;
  text-decoration: none;
  padding-top: 30px;
  padding-left: 20px;
  padding-right: 20px;
  display: inline-block;
  margin: 0 10px;
}

button {
  margin-top: 15px;
  background-color: #85cb6c;
  border: none;
  border-radius: 10px;
  transition: 0.3s;
}

button:hover {
  background-color: black;
  color: #00ff06;
}

button p {
  color: #fff3f3;
  text-decoration: none;
  font-size: 16px;
  font-weight: bold;
}
.logoutbutton {
  margin-left: 10px;
  color: #fff3f3;
  text-decoration: none;
  font-size: 16px;
  font-weight: bold;
}

</style>
