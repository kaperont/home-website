<template>
  <div class="container">
    <div class="row welcome-msg">Welcome back, {{this.user.firstName}}</div>
    <div class="row">
      <div class="col link-title">Github:</div>
      <a class="col" href="https://github.com/kperont/">https://github.com/kperont/</a>
    </div>
    <div class="row">
      <div class="col link-title">Canvas:</div>
      <a class="col" href="https://cedarville.instructure.com">https://cedarville.instructure.com</a>
    </div>
    <div class="row logout-container">
      <div @click="logout()" class="col logout">Logout</div>
    </div>
  </div>
</template>

<script>
import {User} from '../controllers/data'
import store from '../store/index'

export default {
  store: store,
  data() {
    return {
      user: User
    };
  },
  methods: {
    logout() {
      this.$store.commit("LOGOUT");
      this.$router.push('/login');
    }
  },
  mounted() {
    // Grab the active user ID
    const user = this.$store.getters.getActiveUser;
    if(user != null) {
      this.user = User.UserFromObject(user);
    }
  },
  beforeCreate() {

    if(this.$store.getters.getActiveUser == null){ 
        this.$router.push('/login');
    }
    else {
      // Grab the active user ID
      const user = this.$store.getters.getActiveUser;
      this.user = User.UserFromObject(user);
    }
  }
}
</script>

<style scoped>
.welcome-msg {
  justify-content: center;
  font-family: luminari;
  font-size: 50px;
  font-weight: bold;
  margin-top: 1.5em;
  margin-bottom: 1.5em;
}

.link-title {
  text-align: right;
  font-family: luminari;
  font-weight: bold;
}

.logout-container {
  justify-content: center;
  text-align: center;
  margin: auto;
  margin-top: 3em;
  width: 6em;
  height: 2em;
  background-color: green;
  border-radius: 20px;
}

.logout-container:hover {
  opacity: 90%;
}

.logout {
  font-family: luminari;
  font-weight: bold;
  justify-content: center;
  text-align: center;
  margin: auto;
}
</style>
