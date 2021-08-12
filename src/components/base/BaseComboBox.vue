<template>
  <div class="drop-down">
    <div class="drop-down-box" data-id="1">
      <input
        type="text"
        placeholder="Chọn/Nhập thông tin"
        class="combo-box-input"
        v-bind:filter="type"
        v-model="this.dataCombobox.Name"
        v-if="mode == 1"
      />
      <div
        class="drop-down-icon"
        id="position-form-icon"
        v-on:click="showDataCombobox"
      >
        <i class="fas fa-chevron-down"></i>
      </div>
    </div>
    <ul
      class="drop-down-list Position-form"
      v-bind:class="{ 'combobox-data-active': isActive }"
    >
      <li
        class="drop-down-item"
        v-for="item in items"
        :key="item[typeName]"
        @click="getItem(item[typeId], item[typeName])"
      >
        <!-- <div class="tick-item">

                    </div> -->
        <span> {{ item[typeName] }}</span>
      </li>
    </ul>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Combobox",
  props: {
    dataCombobox: {
      type: Object,
      required: false,
      default() {
        return {};
      },
    },
    type: {
      type: String,
      default: function () {
        return "";
      },
    },
    api: {
      type: String,
      default: function () {
        return "";
      },
    },
    data: {
      type: Array,
      default: function () {
        return [];
      },
    },
    mode: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      isActive: false,
      value: "",
      current: 0,
      isDataLoaded: false,
      typeName: this.type + "Name",
      typeId: this.type + "Id",
      items: this.data,
      map: {
        Position: " Vị trí",
        Department: " Phòng ban",
        Gender: "Giới tính",
        WorkStatus: "Trạng thái",
      },
    };
  },
  created() {
    if (!this.items.length) {
      axios
        .get(this.api)
        .then((res) => {
          //console.log(res);
          this.items = [];
          if (this.mode == 1) {
            this.items.push({
              [this.typeName]: "Tất cả" + this.map[this.type],
            });
          }
          res.data.forEach((element) => {
            this.items.push(element);
          });
        })
        .catch((err) => {
          console.log(err);
        });
    }
  },
  methods: {
    showDataCombobox() {
      this.isActive = !this.isActive;
      console.log("click");
      // console.log(this.items);
    },
    getItem(itemId, name) {
      //   console.log(itemId);
      //   console.log(name);
      // debugger;
      this.$emit("department", itemId, name);
      this.$emit("position", itemId, name);
      this.$emit("gender", itemId, name);
      this.$emit("workstatus", itemId, name);
      this.isActive = !this.isActive;
    },
  },
};
</script>
<style scoped>
@import "../../css/common/dropdown.css";
</style>