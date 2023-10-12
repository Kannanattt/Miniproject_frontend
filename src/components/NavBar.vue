<template>
  <v-app-bar app color="primary" dark>
    <div class="d-flex align-center">
      <div
        style="
          background-color: var(--color-main);
          border-radius: 100px;
          width: 40px;
          height: 40px;
          display: flex;
          justify-content: center;
          align-items: center;
          padding-left: 5px;
          margin-right: 10px;
        "
      >
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://clipart-library.com/img1/2026292.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <v-text
        class="shrink mt-1 hidden-sm-and-down"
        style="color: var(--color-main); font-weight: bold"
        contain
        min-width="100"
        width="100"
      >
        <h3>SHOOTINHG</h3>
      </v-text>
    </div>

    <v-spacer></v-spacer>
    <router-link to="/">
      <span :class="{ active: $route.path === '/' }">หน้าแรก</span>
    </router-link>
    <v-spacer></v-spacer>
    <router-link to="/login">
      <span :class="{ active: $route.path === '/login' }">เข้าสู่ระบบ</span>
    </router-link>
  </v-app-bar>
</template>

<script>
export default {
  name: "NavBar",
  data: () => ({}),
};
</script>

<style scoped>
a span {
  text-decoration: none;
  color: var(--color-white);
}

.active {
  color: var(--color-main);
}
</style>