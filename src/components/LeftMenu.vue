<template>
  <div id="realLeft" :style="{width: props.refWidth+'px', left: props.refLeft+'px'}">
    <div id="homeLogo">
      <h1 style="color: black;">
        Fred's
      </h1>
      <h2 style="color: white; background-color: black;">
        Blog >_
      </h2>
    </div>
    <el-button v-for="option in options"
               @click="$emit('switchPage',option.clickParam)"
               :key="option.text" :icon="option.icon" class="menuBtn" size="large" text round>
      {{ option.text }}
    </el-button>

    <el-button round size="large" type="primary" class="menuBtn spBtn" @click="$emit('switchPage','w')">
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;写长博文&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    </el-button>

    <div class="profileBox" @click="$emit('checkLogin')">
      <div class="avaAndName">
        <el-avatar
            :src="loginStatus.logonStatus&&loginStatus.logonProfile.userAvatar
            ?loginStatus.urlStart+loginStatus.logonProfile.userAvatar.formats.thumbnail.url:
            loginStatus.defaultAvatar" class="avatarInline">

        </el-avatar>
        <div id="nameID">
          <div id="userName">
            {{ loginStatus.logonProfile.username }}
          </div>
          <div id="userID">
            {{ '@' + loginStatus.logonProfile.userID }}
          </div>
        </div>
      </div>
      <el-icon class="settingsIcon">
        <MoreFilled/>
      </el-icon>

    </div>
  </div>
</template>

<script setup>

import {ref} from "vue";
import {loginStatus} from "../LogStatus.js";

const props = defineProps({
  refWidth: Number,
  refLeft: Number,
})

let options = [
  {text: "热门", icon: "HotWater", clickParam: 'h'},
  {text: "最新", icon: "Notification", clickParam: 'lb'},
  {text: "我的关注", icon: "Pointer", clickParam: 'f'},
  {text: "日志", icon: "Calendar", clickParam: 's'},
  {text: "README", icon: "Document"}
]

let profile = ref({
  userID: "undefined",
  userName: "undefined",
  userAvatar: 'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
  userRole: undefined
})//预计废弃
defineExpose({
  // 使用setup语法糖需要定义expose来向外暴露属性
  profile
})
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

#realLeft {
  position: fixed;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
}

#homeLogo {
  margin-top: 10px;
  font-family: "Cascadia Code";
}

.menuBtn {
  margin-top: 10px;
  margin-left: 0;
}

.spBtn {
  font-family: "微软雅黑 Light";
  font-weight: bold;
  font-size: 16px;
}

.profileBox {
  //background-color: aqua;
  cursor: pointer;
  border-radius: 25px;
  width: 200px;
  height: 50px;
  position: absolute;
  bottom: 10px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.profileBox:hover {
  background-color: rgba(15, 20, 25, 0.1)
}

.avaAndName{
  display: flex;
  flex-direction: row;
  align-items: center;
}

.avatarInline {
  margin-left: 7px;
}

#nameID {
  font-family: 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB',
  'Microsoft YaHei', '微软雅黑', Arial, sans-serif;
  margin-left: 6px;
}

#userName {
  font-weight: bold;
  margin-bottom: 2px;
}

#userID {
  font-size: 14px;
  color: rgba(0, 0, 0, 0.71);
}

.settingsIcon {
  margin-right: 10px;
}
</style>