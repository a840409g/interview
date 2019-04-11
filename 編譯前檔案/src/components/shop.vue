<template>
  <div class="outer">
    <div class="img">
      <img
        src="https://instagram.ftpe7-3.fna.fbcdn.net/vp/0229d32386e6ce0a7d803a7296382124/5D2F432F/t51.2885-19/s150x150/36149470_632323783802897_6495708564240203776_n.jpg?_nc_ht=instagram.ftpe7-3.fna.fbcdn.net"
        alt
      >
      <div v-if="status=='預購'" class="order">預購數量: {{orderStatus}}</div>
      <!-- 透過status來判斷狀況是否為預購，若是就顯示出來 -->
    </div>
    <div class="panels">
      <div class="panel panel1">倒數時間: {{time}}</div>
      <div class="panel panel2">商品名稱: Joe</div>
      <div class="panel panel3">剩餘數量: {{num}}</div>
      <div @click="showFun()" class="buy">{{status}}</div>
      <div v-if="status != '停售'" class="buy_btn">
        <div @click="endFun($event)" data-num="3" class="cross">X</div>
        <p>我要 {{status}}</p>
        <div class="buy_panel">
          <div @click="countFun($event)" data-num="1" class="buy_click">-</div>
          <div class="buyStatus">{{changeStatus}}</div>
          <div @click="countFun($event)" data-num="2" class="buy_click">+</div>
          <div @click="endFun($event)" class="comfirm">確定</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "shop",
  data() {
    return {
      time: 70,
      num: 10,
      status: "購買",
      orderStatus: 0,
      changeStatus: 0
    };
  },
  created() {
    this.countBack();
    // 讓時間倒數在created的階段自動執行
  },
  methods: {
    countBack() {
      setInterval(() => {
        this.time-=1;
        if (this.time > 60) {
          // console.log(this.time)
          $(".panel1").addClass("blue");
        } else if (0 < this.time && this.time < 60) {
          $(".panel1").addClass("orange");
        } else if (this.time <= 0) {
          // console.log(this.time)
          $(".panel1").addClass("gray");
          $(".buy_btn").css("display", "none");
          this.time = 0;
          this.status = "停售";
        }
      }, 100);
    },
    // 用if來判斷時間並做出想要的動作
    showFun() {
      $(".buy_btn").css("display", "block");
    },
    // 若status是停售狀態就無法顯示購買框
    endFun(e) {
      let data = e.target.dataset.num;
      if(data == 3){
        $(".buy_btn").css("display", "none");
      }else if (this.num <= 0) {
        this.status = "預購";
        this.orderStatus += this.changeStatus;
        this.num = 0;
        this.changeStatus = 0;
        console.log(this.num);
      } else {
        this.num -= this.changeStatus;
        this.changeStatus = 0;
        console.log(this.num);
      }
      $(".buy_btn").css("display", "none");
    },
    // 根據num的狀態來改變status的狀態,再透過changeStatus的數字來改變預購數量或者商品數量
    // 是減商品或是增加預購數量也是按照商品數量num來判斷
    countFun(e) {
      let data = e.target.dataset.num;
      // console.log(data)
      if (data == 1) {
        this.changeStatus -= 1;
      } else if (data == 2) {
        this.changeStatus += 1;
      }
      console.log(this.changeStatus);
    }
    // 從data來判斷加減與否,然後做出相對應的動作
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.outer {
  border: 1px solid #000;
  width: 800px;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.img {
  border: 1px solid #000;
  width: 350px;
  height: 350px;
}
img {
  width: 100%;
  height: 100%;
}
.panels {
  /* border: solid 1px black; */
  display: inline-block;
  align-items: center;
  margin-left: 50px;
  position: relative;
}

.panel {
  border: solid 1px black;
  width: 300px;
  margin-bottom: 50px;
  height: 50px;
  line-height: 50px;
}
.blue {
  border: 5px solid blue;
}
.orange {
  border: 5px solid orange;
}
.gray {
  border: 5px solid gray;
}
.buy {
  border: 1px solid #000;
  width: 80px;
  margin-left: 220px;
  cursor: pointer;
  height: 50px;
  line-height: 50px;
}
.buy_btn {
  border: 1px solid #000;
  background-color: gray;
  width: 300px;
  height: 200px;
  position: absolute;
  top: 100px;
  right: 150px;
  display: none;
}
.cross {
  position: absolute;
  color: #d4f4dd;
  font-weight: 700;
  right: 20px;
  top: 10px;
  font-size: 32px;
  cursor: pointer;
}
p {
  color: #000;
  font-weight: 700;
  font-size: 26px;
}
.buy_panel {
  display: inline-flex;
  -ms-flex-align: center;
  align-items: center;
  padding: 0 20px;
  position: relative;
}
.buy_click {
  background-color: #fff;
  line-height: 20px;
  font-size: 30px;
  height: 20px;
  width: 20px;
  padding: 10px;
  cursor: pointer;
}
.buyStatus {
  font-size: 64px;
  line-height: 64px;
  padding: 0 30px;
}
.comfirm {
  border: 1px solid #000;
  background-color: #fff;
  width: 100px;
  height: 30px;
  line-height: 30px;
  position: absolute;
  bottom: -40px;
  left: 50%;
  transform: translate(-50%);
  cursor: pointer;
}
.order {
  width: 100px;
  position: absolute;
  top: 50px;
  right: 320px;
}
</style>
