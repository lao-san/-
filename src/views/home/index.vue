<template>
  <el-container class="llContainer">
    <el-header class="llHeader wrap" style="height:30px">
      <div class="right user">
        <el-dropdown size="small">
          <span class="el-dropdown-link">
            用户名称
            <i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>个人中心</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </el-header>
    <!-- 主题内容 -->
    <el-main class="llMain wrap">
      <div class="top">
        <el-row>
          <el-col :span="17">
            <div class="grid-content bg-purple">
              <div class="fz_20">XXXXX学术研讨会</div>
              <div class="fz_20">ABCDFWERDFSGFGJHKCXBFGJHKUUOIODFGDFGDFG</div>
              <div class="fz_14">2020年1月1日至2020年1月3日</div>
              <div class="fz_14">国家会议中心3号厅</div>
            </div>
          </el-col>
          <el-col :span="7">
            <div class="grid-content bg-purple-light fontCenter">
              <div>距离会议开幕还有</div>
              <div class="time">{{countDownList}}</div>
            </div>
          </el-col>
        </el-row>
      </div>
      <div class="bottom">
        <el-row>
          <el-col :span="17">
            <div class="grid-content bg-purple">1</div>
          </el-col>
          <el-col :span="7">
            <div class="grid-content bg-purple-light">2</div>
          </el-col>
        </el-row>
      </div>
    </el-main>
  </el-container>
</template>
<script>
export default {
  name: "",
  data() {
    return {
      countDownList: "00天00时00分00秒",
      actEndTime: "2020-1-20 17:03:00"
    };
  },
  components: {},
  computed: {},
  beforeMount() {},
  mounted() {
    this.countDown(); //倒计时
  },
  methods: {
    timeFormat(param) {
      return param < 10 ? "0" + param : param;
    },
    countDown() {
      var interval = setInterval(() => {
        // 获取当前时间，同时得到活动结束时间数组
        let newTime = new Date().getTime(); // 对结束时间进行处理渲染到页面
        let endTime = new Date(this.actEndTime).getTime();
        let obj = null; // 如果活动未结束，对时间进行处理
        if (endTime - newTime > 0) {
          let time = (endTime - newTime) / 1000; // 获取天、时、分、秒
          let day = parseInt(time / (60 * 60 * 24));
          let hou = parseInt((time % (60 * 60 * 24)) / 3600);
          let min = parseInt(((time % (60 * 60 * 24)) % 3600) / 60);
          let sec = parseInt(((time % (60 * 60 * 24)) % 3600) % 60);
          obj = {
            day: this.timeFormat(day),
            hou: this.timeFormat(hou),
            min: this.timeFormat(min),
            sec: this.timeFormat(sec)
          };
        } else {
          // 活动已结束，全部设置为'00'
          obj = {
            day: "00",
            hou: "00",
            min: "00",
            sec: "00"
          };
          clearInterval(interval);
        }
        this.countDownList =
          obj.day + "天" + obj.hou + "时" + obj.min + "分" + obj.sec + "秒";
      }, 1000);
    }
  },

  watch: {}
};
</script>
<style scoped lang='scss'>
.left {
  float: left;
}
.right {
  float: right;
}
.fz_14 {
  font-size: 14px;
}
.fz_20 {
  font-size: 20px;
  font-weight: 1000;
}
.wrap {
  width: 1100px;
  margin: 0 auto;
}
.fontCenter {
  text-align: center;
}
.llContainer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #f0f4f7;
  .llHeader {
    .user {
      margin-right: 100px;
      line-height: 30px;
    }
    .el-dropdown-link {
      cursor: pointer;
      color: #409eff;
    }
  }
  .llMain {
    padding: 0;
    .top {
      height: 100px;
      padding: 10px;

      .time {
        line-height: 70px;
      }
    }
    .bottom {
      border: 1px solid red;
    }
  }
}
</style>

