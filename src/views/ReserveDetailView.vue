<template>
    <v-container style="padding-top: 50px; padding-bottom: 60px">
    <v-btn text @click="$router.go(-1)" style="margin-bottom: 20px">
      <v-icon left>mdi-arrow-left</v-icon> ย้อนกลับ
    </v-btn>
    <v-row justify="center" style="margin-top: 20px">
      <h2>ข้อมูลการจอง</h2>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" xs="12" sm="12" md="12">
        <v-card style="margin: 20px" class="card" v-if="items">
          <v-card-title>{{ items.shootingRange.s_name }}</v-card-title>
          <v-card-text>{{ items.r_date_reserve }}</v-card-text>
          <v-card-text>{{ items.r_time_reserve }}</v-card-text>
          <v-card-text> ปืน </v-card-text>
          <v-card-text v-for="gun in items.guns" :key="gun.id">{{
            gun
          }}</v-card-text>
        </v-card>
        <v-card style="margin: 20px" class="card" v-if="!items">
          <v-card-title>ยังไม่มีข้อมูลการจองสนาม</v-card-title>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      auth: "",
      c_id: null,
      items: null,
    };
  },
  created() {
    this.auth = JSON.parse(localStorage.getItem("auth"));
    this.c_id = this.auth.c_id;
    this.getDetail();
  },
  methods: {
    async getDetail() {
      try {
        const response = await this.axios.get(
          process.env.VUE_APP_API_SERVER + `/reserves`
        );
        if (response.status === 200) {
          this.items = response.data.filter(
            (item) => item.customer.c_id === this.c_id
          );
          this.items = this.items[0];
          console.log("items", this.items);
        }
      } catch (error) {
        console.error("Registration error:", error);
      }
    },
  },
};
</script>
<style scoped>
a {
  text-decoration: none;
}

a:hover .card {
  background-color: var(--color-main);
}
</style>
