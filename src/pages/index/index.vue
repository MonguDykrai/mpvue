<template>
  <div>
    <!-- <div @click="clickHandle"> -->
    <div class="userinfo" @click="bindViewTap">
      <img
        class="userinfo-avatar"
        v-if="userInfo.avatarUrl"
        :src="userInfo.avatarUrl"
        background-size="cover"
      >
      <img class="userinfo-avatar" src="/static/images/user.png" background-size="cover">

      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" :value="motto" placeholder="v-model">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model">
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy">
    </form>

    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>

    <div class="all">
      <div class="left"></div>
      <div class="right"></div>
    </div>

    <h1>Todo List</h1>

    <ul class="list">
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed">
        <!-- <span>{{ todo.userId }}</span> -->
        <!-- <span>{{ todo.id }}</span> -->
        <p class="ellipsis">{{ todo.title }}</p>
        <!-- <span>{{ todo.completed }}</span> -->
      </li>
    </ul>
  </div>
</template>

<script>
import card from "@/components/card";

// console.log("%cwx: ", "color: red;");
// console.log(wx);

// console.log({
//   global,
//   mpvue,
//   mpvuePlatform,
//   getApp
// });

export default {
  data() {
    return {
      motto: "Hello miniprograme",
      userInfo: {
        nickName: "mpvue",
        avatarUrl: "http://mpvue.com/assets/logo.png"
      },
      todos: [],
      checked: false,
    };
  },

  components: {
    card
  },

  methods: {
    bindViewTap() {
      // wx.showLoading({
      //   title: "确定是否要离开本页",
      //   false: true
      // });

      // mpvue.showToast({
      //   title: "hello world"
      // });

      // return;

      const url = "../logs/main";
      if (mpvuePlatform === "wx") {
        mpvue.switchTab({ url });
      } else {
        mpvue.navigateTo({ url });
      }
    },

    clickHandle(ev) {
      console.log("clickHandle:", ev);
      // throw {message: 'custom test'}
    }
  },

  created() {
    // let app = getApp()
    // this.$http
    //   .get("https://api.douban.com/v2/movie/top250?start=25&count=25")
    //   .then(res => {
    //     console.log(res);
    //   })
    //   .catch(err => {
    //     console.error(err);
    //   });

    this.todos = require("./data.json");
    // this.todos.forEach(todo => {
    //   console.log(todo);
    // });
  }
};
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all {
  width: 7.5rem;
  height: 1rem;
  background-color: blue;
}
.all:after {
  display: block;
  content: "";
  clear: both;
}
.left {
  float: left;
  width: 3rem;
  height: 1rem;
  background-color: red;
}

.right {
  float: left;
  width: 4.5rem;
  height: 1rem;
  background-color: green;
}
</style>

<style lang="scss" scoped>
h1 {
  height: 30px;
  line-height: 30px;
  text-align: center;
}

.list {
  // background-color: red;

  > li {
    display: flex;
    padding: 10px 12px;
  }
}

.ellipsis {
  // https://css-tricks.com/almanac/properties/t/text-overflow/
  text-overflow: ellipsis;

  /* Required for text-overflow to do anything */
  white-space: nowrap;
  overflow: hidden;
}
</style>