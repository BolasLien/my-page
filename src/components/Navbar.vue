<template>
  <div id="navbar">
    <!-- logo與登入登出 -->
    <b-container>
      <b-row class="align-items-center">
        <b-col class="links" cols="4">
          <a href="https://www.instagram.com/mini.attic/">
            <font-awesome-icon :icon="['fab','instagram']" size="lg"></font-awesome-icon>
          </a>
          <span>&ensp;|&ensp;</span>
          <router-link to="/">
            <font-awesome-icon :icon="['fab','facebook-square']" size="lg"></font-awesome-icon>
          </router-link>
        </b-col>
        <b-col class="logo" cols="4">
          <router-link to="/">
            <b-img :src="require('../assets/logo.png')" width="100" center></b-img>
          </router-link>
        </b-col>
        <b-col class="login" cols="4">
          <router-link to="/reg" v-if="user.length===0 || user === undefined">
            <font-awesome-icon :icon="['fas','user']" size="lg"></font-awesome-icon>
            <span class="hidden-md">註冊</span>
          </router-link>
          <router-link to="/order" v-else>
            <font-awesome-icon :icon="['fas','list-alt']" size="lg"></font-awesome-icon>
            <span class="hidden-md">訂單管理</span>
          </router-link>
          <span>&ensp;|&ensp;</span>

          <router-link to="/login" v-if="user.length===0 || user === undefined">
            <font-awesome-icon :icon="['fas','sign-in-alt']" size="lg"></font-awesome-icon>
            <span class="hidden-md">登入</span>
          </router-link>
          <a href="#" v-else @click="logout">
            <font-awesome-icon :icon="['fas','sign-out-alt']" size="lg"></font-awesome-icon>
            <span class="hidden-md">登出</span>
          </a>
          <span>&ensp;|&ensp;</span>

          <router-link to="/cart">
            <font-awesome-icon :icon="['fas','shopping-cart']" size="lg"></font-awesome-icon>
            <span class="hidden-md" v-if="cartNum<=0">購物車</span>
            <span v-else>
              <span class="hidden-lg">共</span>
              {{cartNum}}
              <span class="hidden-lg">件商品</span>
            </span>
          </router-link>
        </b-col>
      </b-row>
    </b-container>
    <!-- Navigation -->
    <div>
      <b-navbar toggleable="sm">
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="m-auto">
            <b-nav-item to="/About">關於我們</b-nav-item>
            <b-nav-item to="/Shop">各式甜點</b-nav-item>
            <b-nav-item to="/News">最新消息</b-nav-item>
            <b-nav-item to="/Faq">購買流程</b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Navbar',
  computed: {
    cartNum () {
      return this.$store.getters.cart.totalAmount
    },
    user () {
      return this.$store.getters.user
    }
  },
  methods: {
    logout (event) {
      event.preventDefault()

      this.$axios.logout()
    }
  }
}
</script>
