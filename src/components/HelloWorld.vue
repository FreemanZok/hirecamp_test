<template>
  <div class="">
    <div class="text-center my-container px-4">
      <h2 class="mb-4 py-2">hello, this is a test...</h2>
      <div>
        <v-select
          :items="myItems"
          v-model="chosen"
          item-text="title"
          item-value="stages"
          label="مشاغل"
          solo
        >
        </v-select>
        <!-- <div class="mb-4">
          <div>
            {{ chosen }}
          </div>
        </div> -->
      </div>
      <div class="levels-container">
        <div class="level">
          <div
            v-for="(circle, index) in 7"
            :key="circle"
            class="circle-wrapper"
          >
            <div
              @click="chosen.length ? join_it(index) : ''"
              class="circle mb-3"
              :class="chosen.length > index ? 'active' : ''"
            ></div>
            <div class="text-center">
              {{ chosen[index] }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({
    myItems: [],
    chosen: [],
    e1: 1,
    levels: [
      "منتظر بررسی",
      "کاندید مصاحبه تلفنی",
      "کاندید مصاحبه حضوری",
      "کاندید آزمون عملی",
      "کاندید بررسی منابع انسانی",
      "کاندید بررسی مدیر عامل",
      "کاندید استخدام",
    ],
  }),
  methods: {
    getData() {
      let api = "https://hire.camp/api/job/list";
      this.axios.get(api).then((response) => {
        console.log(response.data);
        this.myItems = response.data;
      });
    },
    join_it(index) {
      let counter = index + 1;
      if (this.chosen.length >= counter) {
        this.chosen = [];

        for (let x = 0; x < index; x++) {
          // switch (x) {
          //   case 0:
          //     break;
          //   case y:
          //     break;
          //   default:
          // }

          this.$set(this.chosen, x, this.levels[x]);
        }
      } else {
        for (let z = this.chosen.length; z < counter; z++) {
          this.$set(this.chosen, z, this.levels[z]);
        }
      }
    },
  },
  created() {
    this.getData();
  },
};
</script>
<style lang="scss" scoped>
.my-container {
  max-width: 800px;
  margin: 0 auto;
  background: rgb(200, 248, 252);
  min-height: 100vh;
}
.level {
  display: flex;
}
.circle-wrapper {
  width: calc(100% / 7);
  // display: flex;
  // justify-content: flex-start;

  .circle {
    border: solid 2px rgb(81, 176, 3);
    height: 70px;
    width: 70px;
    border-radius: 50%;

    &.active {
      background: green;
    }
  }
}
</style>