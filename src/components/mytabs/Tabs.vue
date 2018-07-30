<template>
  <div id="app">
    <div class="radio-wrap">
      <div class="radio-group">
        <span v-for="(tab ,index) in tabs" :key="tab.name" :class="{cur:iscur==index}" @click="iscur=index,tabChange('select' + (index + 1))">{{tab.name}}</span>
      </div>
      <div style="margin:10px 0;"></div>
      <keep-alive>
        <component v-bind:is="tabView"></component>
      </keep-alive>
    </div>
  </div>
</template>

<script>
import select1 from './MyTabs01'
import select2 from './MyTabs02'
import select3 from './MyTabs03'
export default {
  /* eslint-disable */
  name: "Tabs",
  data() {
    return {
      tabView: "select1",
      tabs: [{ name: "选项一" }, { name: "选项二" }, { name: "选项三" }],
      iscur: 0
    };
  },
  components: {
    select1,
    select2,
    select3
  },
  methods: {
    tabChange: function(tab) {
      this.tabView = tab;
    }
  }
};
</script>
 
<style>
.radio-group {
  font-size: 0;
  height: 26px;
  line-height: 26px;
}
.radio-group > span {
  cursor: pointer;
  display: inline-block;
  font-size: 16px;
  text-align: center;
  width: 100px;
}
.cur {
  color: #fff;
  background-color: #20a0ff;
}
</style>
