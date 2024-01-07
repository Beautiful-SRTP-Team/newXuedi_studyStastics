<template >
  <v-container class="count">
    <!-- 签到打卡弹出的对话框 -->
    <v-dialog class="w-25 "
              v-model="open"
              :scrim="false"
              transition="dialog-bottom-transition"
              >
      <!--签到打卡整体入口-->

      <template v-slot:activator="{ props }">
        <div >
          <embed src="../../统计管理.svg" type="image/svg+xml">
          <v-btn
            class="countText"
            color="primary"
            dark
            v-bind="props"
          >
            统计管理
          </v-btn>
        </div>
      </template>

      <!-- 对话框的卡片 -->
      <v-card
        class="mx-auto"
        max-width="800">

        <!-- 打卡文本信息 -->
        <v-card-subtitle class="pt-4">
          统计情况
        </v-card-subtitle>

        <v-card-text class="asd">
          <echarts1/>
        </v-card-text>

        <!-- 打卡事件 -->
        <v-card-actions>
          <v-btn color="orange" @click="open=false">
            关闭
          </v-btn>
        </v-card-actions>

      </v-card>

    </v-dialog>

  </v-container>

  </template>

  <script >

  import echarts1 from "@/components/echarts.vue";
  export default {
    components: {
      echarts1,

    },

    data() {
      return {

        open: false, // 初始化open为false

      };
    },
  };
  </script>

  <style scoped>
  .asd{
    width:800px
  }

    .count{
        float: right;
        width: 12.5vw;
        margin-right: 0vw;
    }
    .count embed{
        margin-left: -1vw;
        margin-top: 1.8vh;
        height: 19vh;
    }
    .count .countText{
        text-align: right;
        margin-right: 4vw;
        font-size: 2.55vh;
        font-family: 黑体;
        font-weight: 900;
    }
  </style>
