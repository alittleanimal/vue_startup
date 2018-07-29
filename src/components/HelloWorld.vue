<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <p v-if="isExisted">isExisted is true</p>
    <div v-else>isExisted is false</div>
    <div v-show="isShown">display the element</div>
    <div>
      <ul>
        <li v-for="(item, itemIndex) in items" :key="item.name">{{itemIndex}}--{{item.name}}</li>
        <li v-for="val in 10" :key="val">{{val}}</li>
      </ul>
    </div>
    <button @click="press">press</button>
    <button @click="count++">{{count}}</button>
    <input type="text" v-model="username">
    <input type="text" v-model="password">
    <button :class="[canSubmit ? 'active': 'unactive']" @click="submit">submit</button>
    <p>{{picked}}</p>
    <input type="checkbox" name="" v-model="picked" value="1" id="1">
    <input type="checkbox" name="" v-model="picked" value="2" id="2">
    <input type="checkbox" v-model="checked" value="1">
    <input type="checkbox" v-model="checked" value="2">
    <div :inner-text.prop="text"></div>
    <div :style="{ marginTop: '5px', 'margin-bottom': '10px'}">world</div>
    <input type="text" v-model="yuan" placeholder="please input value">
    {{yuan}}
    {{cents}}
    <div v-if="myDir" v-my-directive>{{msg}}</div>
    <img v-lazy="img_url">
  </div>
</template>

<script>
export default {
  /* eslint-disable */
  name: "HelloWorld",
  data() {
    return {
      isExisted: false,
      msg: "Welcome to Your Vue.js App",
      isShown: true,
      items: [
        { id: 1, name: "v-if" },
        { id: 2, name: "v-else" },
        { id: 3, name: "v-show" },
        { id: 4, name: "v-for" }
      ],
      noRoot: false,
      count: 0,
      username: "",
      picked: [],
      checked: [],
      text: "hello",
      isActive: false,
      password: "",
      cents: 100,
      myDir: true,
      img_url: 'https://jingdiaoxike.cn/static/site/img/nav__logo.png'
    };
  },
  computed: {
    canSubmit: function() {
      return this.username && this.password;
    },
    yuan: {
      set: function(val) {
        this.cents = parseInt(val * 100);
      },
      get: function(val) {
        return this.cents / 100;
      }
    }
  },
  methods: {
    press: function() {
      alert("pressed");
    },
    submit: function() {
      if (!this.canSubmit) {
        alert("lack information");
        return;
      }
      alert("submit");
    }
  },
  directives: {
    "my-directive": {
      bind: function(el, binding, vnode, oldVnode) {
        console.log("bind");
      },
      inserted: function(el, binding, vnode, oldVnode) {
        console.log("inserted");
      },
      update: function(el, binding, vnode, oldVnode) {
        console.log("update");
      },
      componentUpdated: function(el, binding, vnode, oldVnode) {
        console.log("componentUpdated");
      },
      unbind: function(el, binding, vnode, oldVnode) {
        console.log("unbind");
      }
    },
    'lazy': {
      inserted: function (el, binding) {
        var body = document.body;
        var offsetTop = el.offsetTop;
        var parent = el.offsetParent;

        while (parent && parent.tagName != 'body') {
          offsetTop += parent.offsetTop;
          parent = parent.offsetParent;
        }

        if (body.scrollTop + body.clientHeight > offsetTop && body.scrollTop < offsetTop) {
          el.src = binding.value;
        } else {
          var scrollFn = function () {
            if(body.scrollTop + body.clientHeight > offsetTop && body.scrollTop < offsetTop) {
              el.src = binding.value;
              window.removeEventListener('scroll', scrollFn)
            }
          }
          window.addEventListener('scroll', scrollFn);
        }
      }
    }
  }
  /* eslint-disable */
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
