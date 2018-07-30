<template>
  <el-container>
    <el-header>Web聊天室(30)</el-header>
    <el-main id="chat-container">
      <div class="type-time">2018年7月24日17:40:32</div>
      <div class="type-msg type-other">
        <div class="images"></div>
        <div class="name">671</div>
        <div class="content">
          <div>你们好呀！</div>
        </div>
      </div>
      <div class="type-time">2018年7月24日17:40:32</div>
      <div class="type-msg type-self">
        <div class="images"></div>
        <div class="name">671111</div>
        <div class="content">
          <div>你哦啊是否hi哦回复</div>
        </div>
      </div>
      <div class="type-msg type-self">
        <div class="images"></div>
        <div class="name">671111</div>
        <div class="content">
          <div>你哦啊是否hi哦回复</div>
        </div>
      </div>
      <div class="type-msg type-other">
        <div class="images"></div>
        <div class="name">671</div>
        <div class="content">
          <div>你们好呀！</div>
        </div>
      </div>
    </el-main>
    <el-aside width="200px">
      <div>在线人数：30</div>
      <div>身份：151</div>
      <div>身份：65</div>
    </el-aside>
    <el-footer height="130px">
      <div class="tool-group">
        <div
          v-for="(item, index) in tool"
          v-bind:key="index">
          <i :class="item"></i>
        </div>
      </div>
      <div class="edit">
        <textarea id="editor"></textarea>
      </div>
      <div class="btn-group">
        <el-button size="small" @click="clearEdit">清空(C)</el-button>
        <el-button type="primary" size="small" @click="sendData">发送(S)</el-button>
      </div>
    </el-footer>
  </el-container>
</template>

<script>
import $ from 'jquery'

export default {
  name: 'Index',
  data () {
    return {
      tool: [
        'el-icon-view',
        'el-icon-service'
      ],

      // 滚动条高度
      sh: 0
    }
  },
  mounted () {
    var _this = this

    // 键盘事件
    $(document).keydown((ev) => {
      if (ev.keyCode === 13) {
        _this.sendData()
      }
      if (ev.ctrlKey && ev.keyCode === 46) {
        _this.clearEdit()
      }
      if (ev.ctrlKey && ev.keyCode === 73) {
        $('#editor').focus()
      }
    })

    // 设置滚动条高度
    this.sh = $('#chat-container')[0].scrollHeight

    // 滚动条往下走
    $('#chat-container').scrollTop($('#chat-container')[0].scrollHeight)
  },
  methods: {
    // 清空输入框
    clearEdit () {
      $('#editor').val('')
      $('#editor').focus()
    },

    // 发送数据
    sendData () {
      // $('#chat-container').append(this.typeTime('2018年7月25日10:34:42'))
      if ($('#editor').val() === null ||
        $('#editor').val() === '') {
        this.$message.error('不能发送空信息！')
      } else {
        // 发送数据
        $('#chat-container').append(this.typeSelf('671', $('#editor').val()))
        $('#editor').val('')
        $('#editor').blur()
      }

      this.isScroll()
    },

    // 时间类型
    typeTime (time) {
      return `
        <div class="type-time">${time}</div>`
    },

    // 我自己记录
    typeSelf (name, text) {
      return `
      <div class="type-msg type-self">
        <div class="images"></div>
        <div class="name">${name}</div>
        <div class="content">
          <div>${text}</div>
        </div>
      </div>`
    },

    // 他人的记录
    typeOther (name, text) {
      return `
      <div class="type-msg type-other">
        <div class="images"></div>
        <div class="name">${name}</div>
        <div class="content">
          <div>${text}</div>
        </div>
      </div>`
    },

    // 出现滚动条的时候
    isScroll () {
      var iSh = $('#chat-container')[0].scrollHeight

      if (iSh > this.sh) {
        // 设置头像左移
        $('.type-self .images').css('left', '552px')

        // 滚动条往下走
        $('#chat-container').scrollTop(iSh)
      }
    }
  }
}
</script>

<style lang="scss">
$border: 1px solid #e5e5e5;

.clearfix:after {
  content: ".";
  clear: both;
  display: block;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}
.el-container {
  width: 840px;
  height: 600px;
  margin: 50px auto;
  position: relative;
  border: 1px solid #e5e5e5;
  box-shadow: 0px 0px 20px #ccc;
  border-radius: 5px;

  .el-header {
    background: #EAE8F1;
    height: 60px;
    line-height: 60px;
    font-size: 20px;
  }

  .el-main, .el-footer {
    width: 640px;
    float: left;
  }

  .el-main {
    height: 400px;
    font-size: 12px;

    div {
      margin-bottom: 5px;
    }

    .type-msg {
      position: relative;

      .images {
        width: 30px;
        height: 30px;
        background: red;
        border-radius: 50%;
        position: relative;
        z-index: 1;
      }
      .name {
        position: absolute;
        top: 3px;
      }
      .content {
        position: relative;
        top: -15px;

        div {
          padding: 8px;
          max-width: 510px;
          margin: 0 auto;
          display: inline-block;
          background: #FDEBC8;
          float: left;
          border-radius: 5px;
          text-align: left;
        }
      }
      .content:after {
        content: '.';
        height: 0;
        clear: both;
        display: block;
        overflow: hidden;
        visibility: hidden;
      }
      .content:before {
        position: absolute;
        content: "";
        width: 0;
        height: 0;
      }
    }
    .type-self {
      .images {
        left: 570px;
      }
      .name {
        right: 35px;
      }
      .content {
        div {
          float: right;
          margin-right: 37px;
          background: #E5E5E5;
        }
      }
      .content:before {
        right: 31px;
        top: 2px;
        border-top: 0 solid transparent;
        border-left: 10px solid #E5E5E5;
        border-bottom: 10px solid transparent;
      }
    }
    .type-other {
      .name {
        left: 35px;
      }
      .content {
        margin-left: 37px;
      }
      .content:before {
        left: -6px;
        top: 2px;
        border-top: 0 solid transparent;
        border-right: 10px solid #FDEBC8;
        border-bottom: 10px solid transparent;
      }
    }
  }

  .el-footer {
    border-top: $border;
    position: relative;

    .tool-group {
      height: 24px;
      width: 630px;
      position: absolute;
      left: 0;
      padding: 0 5px;

      div {
        height: 24px;
        line-height: 24px;
        width: 24px;
        float: left;
        cursor: pointer;
      }
      div:hover {
        background: #e5e5e5;
      }
    }
    .edit {
      textarea {
        width: 620px;
        position: absolute;
        left: 5px;
        top: 25px;
        height: 54px;
        resize: none;
        border: 0;
        outline:none;
      }
    }

    .btn-group {
      .el-button {
        position: absolute;
        bottom: 10px;
      }
      .el-button:nth-child(1) {
        right: 90px;
      }
      .el-button:nth-child(2) {
        right: 10px;
      }
    }
  }

  .el-aside {
    height: 538px;
    position: absolute;
    right: 0;
    top: 60px;
    border-left: $border;

    div:nth-child(1) {
      position: fixed;
      background: #FFF;
      width: 120px;
      padding: 10px 5px;
    }
    div:nth-child(1):hover {
      background: #fff;
    }
    div:nth-child(2) {
      margin-top: 39px;
    }
    div {
      text-align: left;
      font-size: 14px;
      cursor: pointer;
      padding: 2px 5px;
    }
    div:hover {
      background: #f5f5f5;
    }
  }
}
</style>
