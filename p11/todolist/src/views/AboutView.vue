<template>
  <div class="home">
    <div class="box">
      <div class="top">
        <img src="../../public//Snipaste_2023-11-07_10-44-44.png" alt="" />
        <span>今日TODO</span>
      </div>
      <h3>~今天我需要做的事情~</h3>
      <div class="inp">
        <input type="text" v-model="inp" placeholder="请输入今天未完成的list" />
        <button class="add" @click="add">添加</button>
      </div>
      <div class="list">
        <div class="lis" v-for="(item, index) in list" :key="index">
          <div class="li" v-if="tab == 0">
            {{ item.title }}
          </div>
          <div class="li" v-else-if="item.falg == tab">
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
</template>

<script>
export default {
  data() {
    return {
      inp: "",
      tab: 0,
      list: [
        { title: "第一条", falg: 2 },
        { title: "第二条", falg: 1 },
        { title: "已完成", falg: 2 },
      ],
    };
  },
  methods: {
    add() {
      if (this.inp == "") {
        alert("不能为空");
        return false;
      } else {
        this.list.push({ title: this.inp, falg: 1 });
        this.inp = "";
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
  components: {},
  filters: {},
  watch: {},
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100vh;
  padding-top: 10px;
  box-sizing: border-box;
  background: linear-gradient(to right, #f3b2bd, #f6c5a5);

  .box {
    width: 350px;
    height: 95%;
    margin: auto;
    border-radius: 5px;
    background: #fff;
    padding: 0 30px;
    box-sizing: border-box;

    .top {
      width: 100%;
      display: flex;
      justify-content: center;

      img {
        width: 80px;
        margin: 10px;
        // vertical-align: middle;
      }

      span {
        width: 80px;
        height: 20px;
        margin-top: 30px;
        text-align: center;
        font-size: 12px;
        border: 0;
        border-radius: 5px;
        color: #fff;
        background: #ed7b52;
        transform: skewY(3deg);
      }
    }

    h3 {
      text-align: center;
    }

    .inp {
      width: 100%;

      display: flex;
      justify-content: center;
      margin: 15px 0;

      input {
        width: 200px;
        border: 0;
        border-bottom: 2px dashed #ed7b52;
        outline: 0;
      }

      .add {
        width: 60px;
        height: 20px;
        border: 1.5px solid #000;
        border-radius: 5px;
        color: #000;
        background: #fff;
        margin: 0 5px;
        transform: skewY(2deg);
      }
    }

    .list {
      width: 100%;

      .li {
        width: 100%;
        height: 25px;
        color: #fff;
        margin: 5px auto;
        border-radius: 5px;
        background: #ed7b52;
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
}</style>
