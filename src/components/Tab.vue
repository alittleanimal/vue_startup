<template>
    <div id="app">
        <ul>
            <li v-for="(item, index) in tabs" :key="item" :class="{active:index == num}" @click="tab(index)">{{item}}</li>
        </ul>
        <div class="tabCon">
            <div v-for="(itemCon, index) in tabContents" :key="itemCon" v-show="index == num">
                {{itemCon}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
  /* eslint-disable */
  name: "MyTab",
  el: "#app",
  data() {
    return {
      tabs: ["title1", "title2", "title3"],
      tabContents: ["content1", "content2", "content3"],
      num: 1
    };
  },
  methods: {
      tab(index) {
          this.num = index;
      }
  }
};
</script>

