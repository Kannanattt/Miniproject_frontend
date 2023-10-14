<template>
  <div>
    <ImageCover />
    <v-container>
      <h2>ตารางการจองสนามยิงปืน</h2>
      <label for="date">เลือกวันที่: </label>
      <input type="date" id="date" name="date" v-model="selectedDate" />
      <p>Selected Date: {{ selectedDate }}</p>
      <template>
        <v-table fixed-header height="300px">
          <thead>
            <tr>
              <th class="text-left">ชื่อสนาม</th>
              <th class="text-left">10:00 - 11:00</th>
              <th class="text-left">11:00 - 12:00</th>
              <th class="text-left">12:00 - 13:00</th>
              <th class="text-left">13:00 - 14:00</th>
              <th class="text-left">14:00 - 15:00</th>
              <th class="text-left">15:00 - 16:00</th>
              <th class="text-left">16:00 - 17:00</th>
              <th class="text-left">17:00 - 18:00</th>
              <th class="text-left">18:00 - 19:00</th>
              <th class="text-left">19:00 - 20:00</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in roomData" :key="item.name">
              <td>{{ item.range }}</td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_01)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_01 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_02)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_02 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_03)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_03 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_04)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_04 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_05)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_05 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_06)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_06 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_07)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_07 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_08)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_08 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_09)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_09 }}
                  </div>
                </v-chip>
              </td>
              <td>
                <v-chip
                  label
                  :color="getColor(item.time_10)"
                  style="display: flex; justify-content: center; align-items; center; width: 100px;"
                >
                  <div style="text-align: center">
                    {{ item.time_10 }}
                  </div>
                </v-chip>
              </td>
            </tr>
          </tbody>
        </v-table>
      </template>

      <CardModal
        :modalOpen="modalOpen"
        :selectedRoomData="selectedRoomData"
        @close-modal="modalOpen = false"
      />
    </v-container>
  </div>
</template>

<script>
import ImageCover from "@/components/ImageCover.vue";
import CardModal from "@/components/CardModal.vue";
export default {
  name: "HomeView",
  components: {
    ImageCover,
    CardModal,
  },
  data() {
    return {
      selectedDate: "2023-10-15",
      rangeItems: [],
      reserveItems: [],
      modalOpen: false, // Control the modal's visibility
      selectedRoomData: {}, // Store the data for the selected room
      roomData: [],
    };
  },
  watch: {
    selectedDate: function (data) {
      console.log("data", data);
      this.selectedDate = data;
      this.getReserve();
      this.getReserve();
      this.getAllRange();
      this.getAllRange();
    },
  },

  created() {
    this.getReserve();
    this.getAllRange();
  },

  methods: {
    async getAllRange() {
      try {
        const response = await this.axios.get(
          // Note the use of this.$axios
          process.env.VUE_APP_API_SERVER + `/shootingranges`
        );
        this.rangeItems = response.data;
        // this.getReserve();
        console.log("this.reserveItems", this.reserveItems);
        this.roomData = this.rangeItems.map((item, index) => {
          const time_01 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "10:00 - 11:00"
            );
          });
          console.log("time_01", time_01);
          const time_02 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "11:00 - 12:00"
            );
          });
          const time_03 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "12:00 - 13:00"
            );
          });
          const time_04 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "13:00 - 14:00"
            );
          });
          const time_05 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "14:00 - 15:00"
            );
          });
          const time_06 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "15:00 - 16:00"
            );
          });
          const time_07 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "16:00 - 17:00"
            );
          });
          const time_08 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "17:00 - 18:00"
            );
          });
          const time_09 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "18:00 - 19:00"
            );
          });
          const time_10 = this.reserveItems.filter((t, i) => {
            return (
              item.s_id === t.shootingRange.s_id &&
              t.r_time_reserve === "19:00 - 20:00"
            );
          });
          return {
            range: item.s_name,
            time_01: time_01.length > 0 ? "Not Available" : "Available",
            time_02: time_02.length > 0 ? "Not Available" : "Available",
            time_03: time_03.length > 0 ? "Not Available" : "Available",
            time_04: time_04.length > 0 ? "Not Available" : "Available",
            time_05: time_05.length > 0 ? "Not Available" : "Available",
            time_06: time_06.length > 0 ? "Not Available" : "Available",
            time_07: time_07.length > 0 ? "Not Available" : "Available",
            time_08: time_08.length > 0 ? "Not Available" : "Available",
            time_09: time_09.length > 0 ? "Not Available" : "Available",
            time_10: time_10.length > 0 ? "Not Available" : "Available",
          };
        });
      } catch (err) {
        console.error(err);
      }
    },
    getColor(value) {
      return value === "Available" ? "green" : "red";
    },
    openModal(selectedRoomData) {
      console.log("selectedRoomData", selectedRoomData);
      this.selectedRoomData = selectedRoomData;

      this.modalOpen = true; // Open the modal
    },
    async getReserve() {
      try {
        const response = await this.axios.get(
          process.env.VUE_APP_API_SERVER + "/reserves"
        );
        const data = JSON.stringify(response.data);

        const filteredReservations = JSON.parse(data).filter((item) => {
          return item.r_date_reserve === this.selectedDate;
        });

        this.reserveItems = filteredReservations;
        // this.reserveItems = data;
        console.log("reserveItems", this.reserveItems);
      } catch (err) {
        console.error(err);
      }
    },
  },
};
</script>

<style scoped>
.text-left {
  width: 200px;
  font-size: 12px;
  text-align: center;
}

td {
  padding-top: 10px;
}
</style>
