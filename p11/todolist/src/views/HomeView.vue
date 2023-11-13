<template>
  <div class="home">
    <div class="box">
      <div class="top">
        <img src="Snipaste_2023-11-07_10-44-44.png" alt="">
        <span>今日TODO</span>
      </div>
      <h2 style="text-align: center; margin-bottom: 15px;">~今天我需要做的事~</h2>
      <div class="content">
        <div class="text">
          <input v-model="input" type="text" placeholder="请输入未完成的list">
          <button class="d" @click="add">添加</button>
        </div>
        <div class="list">
          <div class="lis" v-for="(item, index) in list" :key="index">
            <div class="li" v-if="tab == 0">
              {{ item.title }}
            </div>
            <div class="li" v-else="item.falg == tab">
              <span @click="cut(index)">√</span>
              {{ item.title }}
            </div>
          </div>
        </div>
        <div class="tab">
          <span>{{ list.length == 0 ? "无事项" : sum + "个事项" }}</span>
          <span :class="tab == 0 ? 'xz' : ''" @click="tab = 0">查看所有</span>
          <span :class="tab == 1 ? 'xz' : ''" @click="tab = 1">待完成</span>
          <span :class="tab == 2 ? 'xz' : ''" @click="tab = 2">已完成</span>
          <span @click="dels">清空所有</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  //存放数据
  data() {
    return {
      input: "",
      tab: 0,
      list: [
        { title: "第一条", falg: 2 },
        { title: "第二条", falg: 1 },
        { title: "已完成", falg: 2 },
      ],
    };
  },
  //存放方法
  methods: {
    add() {
      if (this.input == "") {
        alert("不能为空");
        return false;
      } else {
        this.list.push({ title: this.input, falg: 1 });
        this.input = "";
      }
    },
    dels() {
      this.list = [];
    },
    cut(i) {
      if (this.list[i].falg == 1) {
        this.list[i].falg = 2;
      } else {
        this.list[i].falg = 1;
      }
    },
  },
  //存放计算属性
  computed: {
    sum() {
      let sum = 0;
      this.list.forEach((ele) => {
        if (this.tab == 0) {
          sum++;
        } else {
          if (ele.falg == this.tab) {
            sum++;
          }
        }
      });
      return sum;
    },
  },
  //创建之后
  created() {
  },
  //存放过滤器
  filters: {

  },
  //存放监听器
  watch: {

  },
  //注册组件
  components: {

  },
};
</script>

<style lang="scss" scoped>
.home {
  margin: 0;
  background-color: #f5bab5;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  .box {
    border-radius: 10px;
    width: 350px;
    height: 90%;
    background-color: #fff;
  }

  .top {
    text-align: center;
    margin: 20px;
    display: flex;
    justify-content: center;
    align-items: center;

    img {
      width: 90px;
    }

    span {
      transform: rotate(7deg);
      padding: 3px 10px;
      border-radius: 5px;
      background-color: #ed7b52;
      color: #fff;
      font-size: 14px;
    }
  }

  .content {
    margin: auto;
    width: 75%;

    .text {
      input {
        width: 70%;
        border: none;
        border-bottom: #ed7b52 2px dashed;
        height: 20px;
        outline: none;
      }

      button {
        width: 60px;
        padding: 3px 10px;
        background-color: #fff;
        border: solid 1px;
        border-radius: 6px;
        font-weight: 700;
        margin-left: 10px;
        transform: rotate(8deg);
      }

      .d:hover {
        // transform: ;
        transform: scale(1.1) rotate(8deg);
      }
    }

    .tab {
      width: 100%;
      display: flex;
      justify-content: space-around;

      span {
        width: 50px;
        height: 20px;
        line-height: 20px;
        font-size: 11px;
        border-radius: 5px;
        text-align: center;
        color: #000;
        background: #fff;
      }

      .xz {
        color: #fff;
        background: #ed7b52;
      }
    }
  }
}

.list {
  width: 100%;
  margin-top: 20px;
  .li {
    width: 100%;
    height: 25px;
    color: #fff;
    margin: 5px auto;
    border-radius: 5px;
    background: #ed7b52;
  }
}
</style>