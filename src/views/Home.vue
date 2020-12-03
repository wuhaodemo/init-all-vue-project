<template>
  <div class="home">
    <div class="item-wrap" ref="wrap">
      <div class="item" v-for="(item, index) in 20" :key="index" ref="box">
        {{ item }}
      </div>
    </div>

    <div class="list">
      <div
        class="num"
        v-for="(item, index) in 10"
        :key="index"
        :class="{ active: index == activeIndex }"
        @click="scrollTo(index)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
  data() {
    return {
      list: new Array(10),
      activeIndex: 0,
      scrollTop: 0,
      windowHeight: document.body.clientHeight,
    };
  },
  created() {
    this.heightList = [];
  },
  mounted() {
    // this.windowHeight = document.body.clientHeight;
    window.addEventListener("scroll", this.handleScroll, true);
    this.getHeightList();
  },
  methods: {
    scrollTo(index) {
      this.activeIndex = index;
      window.scrollTo(0, this.heightList[index]);
    },
    getHeightList() {
      const list = this.$refs.box;
      this.heightList.push(0);
      let height = 0;
      // list.forEach((ele) =>
      for (let i = 0; i < list.length; i++) {
        let itemF = list[i].clientHeight;
        height += itemF;

        this.heightList.push(height);
      }
    },
    handleScroll(e) {
      this.scrollTop =
        e.target.documentElement.scrollTop || e.target.body.scrollTop; // 执行代码
    },
  },
  computed: {},
  watch: {
    scrollTop(newVal) {
      for (let i = 0; i < this.heightList.length; i++) {
        let hh = this.heightList;
        if (hh[i] < newVal) {
          this.activeIndex = i;
        }
      }
    },
  },
};
</script>

<style lang="less" scoped>
.item {
  width: 100px;
  height: 200px;
  // background: blue;
  border: 1px solid red;
}
.list {
  position: fixed;
  right: 20px;
  top: 20px;
  width: 20px;
  height: 190px;
  cursor: pointer;
  .num {
    height: 20px;

    // border: 1px solid red;
  }
}
.active {
  color: red;
}
</style>
