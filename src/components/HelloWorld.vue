<template>
  <div class="rtl">
    <div class="text-center my-container px-4 py-4">
      <!-- <h2 class="mb-4 py-2">hello, this is a test...</h2> -->
      <div>
        <v-select
          :items="myItems.length ? myItems : ''"
          v-model="chosen"
          item-text="title"
          item-value="stages"
          label="مشاغل"
          solo
        >
        </v-select>
      </div>
      {{choisen}}
      <div class="levels-container">
        <div class="level">
          <div
            v-for="(circle, index) in 7"
            :key="circle"
            class="circle-wrapper"
          >
            <div
              @click="chosen.length ? join_it(index) : ''"
              class="circle mb-7"
              :class="chosen.length > index ? 'active' : ''"
            >
              <img
                class="tick"
                src="../assets/check-mark-svgrepo-com.svg"
                alt=""
              />
            </div>
            <div class="small-circle-wrapper mb-2">
              <div
                class="small-circle"
                :class="chosen.length > index ? 'active' : ''"
              ></div>
            </div>
            <div class="text-center">
              {{ levels[index] }}
            </div>
          </div>
        </div>

        <!-- <div class="gray-line"></div> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data: () => ({
    myItems: [],
    e1: 1,
    chosen: [],
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
        // this.chosen = [];
        let bab = this.chosen.length - counter;
        for (let x = 0; x < bab; x++) {
          this.chosen.pop()
        }
      } else {
        for (let z = this.chosen.length; z < counter; z++) {
          this.$set(this.chosen, z, this.levels[z]);
        }
      }
    },
  },
  watch: {
    chosen() {
      // alert(newVal)
    },
  },
  created() {
    this.getData();
  },
};
</script>
<style lang="scss" scoped>
.small-circle-wrapper {
  position: relative;
  &::after {
    content: "";
    width: 84%;
    height: 2px;
    background: gray;
    position: absolute;
    bottom: 9px;
    left: -43%;
  }
}
.small-circle {
  width: 20px;
  height: 20px;
  margin: 0 auto;
  border: solid 4px #adadad;
  border-radius: 50%;
  &.active {
    border: solid 4px #00c59c;
  }
}
.my-container {
  max-width: 800px;
  margin: 0 auto;
  min-height: 100vh;
}
.levels-container {
  box-shadow: 0 0 5px grey;
  border-radius: 7px;
  padding: 30px 0;
  position: relative;
  .gray-line {
    position: absolute;
    width: 86%;
    height: 30px;
    background: red;
    left: 50%;
    transform: translateX(-50%);
  }
}
.level {
  display: flex;
}
.circle-wrapper {
  width: calc(100% / 7);
  .tick {
    display: none;
  }
  .circle {
    border: solid 3px #a7f8dd;
    height: 70px;
    width: 70px;
    border-radius: 50%;
    position: relative;
    margin: 0 auto;
    &.active {
      background: #e0fffc;
      padding-left: 2px;
      padding-top: 1px;
      .tick {
        display: block;
      }
    }
    &.active ~ .small-circle-wrapper {
      .small-circle {
        background: #96ffd1;
        // border-color: rgb(0, 170, 139);
      }
    }
    &::after {
      content: "";
      width: 0;
      height: 0;
      border-left: 7px solid transparent;
      border-right: 7px solid transparent;
      border-top: 10px solid #a7f8dd;
      position: absolute;
      bottom: -11px;
      left: 50%;
      transform: translateX(-50%);
    }
    &:hover {
      cursor: pointer;
    }
  }
  &:last-child {
    .small-circle-wrapper {
      &::after {
        display: none;
      }
    }
  }
}
.rtl {
  direction: rtl;
}
</style>