<template lang="">
    <div>
        <div class="background-popup" :style="{ display: popupState }">
        <div class="popup">
            <div class="title-wrap">
                <div class="title-popup">
                    <p>Hủy thao tác thêm mới</p>
                </div>
                <div class="exit-popup" v-on:click="changeState(1)">
                    <i id="exit-popup" class="fas fa-times"></i>
                </div>
            </div>
            <div class="content-wrap">
                <div class="alert" v-if="type==1">
                    <i class="fas fa-exclamation-triangle"></i>
                    
                </div>
                <div class="warning" v-if="type==0">
                    <i class="fas fa-exclamation-triangle"></i>
                    
                </div>
                <div class="warning" v-if="type==2">
                    <i class="fas fa-exclamation-triangle"></i>
                    
                </div>
                <div class="content-popup">
                    <p v-if="type==0">Bạn có chắc muốn đóng form nhập <span v-if="type==0">"Thêm mới nhân viên"</span > hay không?</p>
                    <p v-if="type==2">Bạn có chắc muốn <span>"Lưu bản ghi"</span> này hay không?</p>
                    <p v-if="type==1">Bạn có chắc muốn <span>"Xóa bản ghi"</span> này hay không?</p>
                </div>
            </div>
            <div class="button-popup">
                <div class="btn-popup btn-continue" v-on:click="changeState(1)" v-if="type == 0||type == 2" >
                    <p>Tiếp tục nhập</p>
                </div>
                <div class="btn-popup btn-close" v-on:click="changeState(1)" v-if="type == 1">
                    <p>Đóng</p>
                </div>
                <div class="btn-popup btn-close" v-on:click="changeState(0)" v-if="type == 0">
                    <p>Đóng</p>
                </div>
                 <div class="btn-popup btn-close" v-on:click="changeState(2)" v-if="type == 2">
                    <p>Lưu</p>
                </div>
                <div
                  class="btn-delete"
                  v-if="type == 1"
                  v-on:click="changeState(3)"
                >
                  <i class="far fa-trash-alt"></i>
                  <p>Xóa</p>
                </div>
            </div>
        </div>
    </div>
    </div>
</template>
<script>
export default {
  name: "Popup",
  props: {
    data: {
      type: String,
      default: function () {
        return "";
      },
    },
    type: {
      type: Number,
      default: 0,
    },
    showPopup: {
      type: Boolean,
    },
  },
  data() {
    return {
      isShow: false,
    };
  },
  methods: {
    changeState(value) {
      //   debugger;
      this.$emit("hidePopup", value);
    },
  },
  computed: {
    popupState() {
      //   debugger;
      if (this.showPopup) {
        return "block";
      } else {
        return "none";
      }
    },
  },
};
</script>
<style lang="">
</style>