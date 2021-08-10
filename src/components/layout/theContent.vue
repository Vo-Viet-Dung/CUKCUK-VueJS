<template>
  <!-- <div> -->
  <div class="content">
    <div class="content-title">
      <div class="content-title-text">Danh sách nhân viên</div>
      <div
        class="content-delete-employee-button"
        :style="{ display: showBtnDelete }"
        @click="btnDeleteClick()"
      >
        <div class="content-delete-employee-button-icon">
          <i class="far fa-trash-alt"></i>
        </div>
        <div class="content-delete-employee-button-text">Xóa nhân viên</div>
      </div>
      <div class="content-add-employee-button" @click="showModalBox()">
        <div class="content-add-employee-button-icon">
          <img src="../../assets/icon/add.png" />
        </div>
        <div class="content-add-employee-button-text" id="open">
          Thêm nhân viên
        </div>
      </div>
    </div>
    <div class="content-option">
      <!-- <div class="content-option-search">
                <div class="content-option-search-icon"></div> -->
      <input
        class="content-option-search-text"
        placeholder="Tìm kiếm theo Mã, tên hoặc Số điện thoại"
      />
      <!-- </div> -->
      <div class="content-option-workspace">
        <!-- <div class="content-option-workspace-text">Tất cả phòng ban</div>
                <div class="content-option-workspace-icon">
                    <i class="fas fa-chevron-down"></i>
                </div> -->
        <!-- <div class="drop-down">
                    <div class="drop-down-box">
                        <input type="text" class="combo-box-input" id="department-input" placeholder="Tất cả phòng ban">
                        <div class="drop-down-icon" id='workspace'>
                            <i class="fas fa-chevron-down " for="dropdown"></i>
                        </div>
                    </div>
                    <ul class="drop-down-list Workspace" for="dropdown-list">
                        
                    </ul>
                </div> -->
        <Combobox
          :api="'http://cukcuk.manhnv.net/api/Department'"
          :type="'Department'"
          :dataCombobox="dataComboboxDepartment"
          :mode="1"
          v-on:department="getDepartment"
        />
      </div>
      <div class="content-option-position">
        <Combobox
          :api="'http://cukcuk.manhnv.net/v1/Positions'"
          :type="'Position'"
          :dataCombobox="dataComboboxPosition"
          :mode="1"
          v-on:position="getPosition"
        />
      </div>

      <div class="content-option-reload">
        <!-- <img src="../../assets/icon/refresh.png" /> -->
      </div>
    </div>
    <div class="grid">
      <!-- <div class="grid-header"> -->
      <table id="tbListDataEmployee" border="0" cellspacing="0">
        <thead class="thead-table">
          <tr>
            <th></th>
            <th>#</th>
            <th>Mã nhân viên</th>
            <th>Họ và tên</th>
            <th>Giới tính</th>
            <th class="align-center">Ngày sinh</th>
            <th>Điện thoại</th>
            <th>Email</th>
            <th>Chức vụ</th>
            <th>Phòng ban</th>
            <th class="align-right">Mức lương cơ bản</th>
            <th>Tình trạng công việc</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="employee in employee"
            :key="employee.EmployeeId"
            @dblclick="dbClickHandle(employee.EmployeeId)"
            @click="tdClickHandle($event, employee.EmployeeId)"
          >
            <td class="table-checkbox"><input type="checkbox" /></td>
            <td>1</td>
            <td>{{ employee.EmployeeCode }}</td>
            <td>{{ employee.FullName }}</td>
            <td>{{ employee.GenderName }}</td>
            <td class="align-center">{{ formatDate(employee.DateOfBirth) }}</td>
            <td>{{ employee.PhoneNumber }}</td>
            <td>{{ employee.Email }}</td>
            <td>{{ employee.PositionName }}</td>
            <td>{{ employee.DepartmentName }}</td>
            <td class="align-right">{{ formatSalary(employee.Salary) }}</td>
            <td>{{ employee.WorkStatus }}</td>
          </tr>
        </tbody>
      </table>
      <!-- </div> -->
      <div>
        <ModalBox
          :isSave="modalIsSave"
          :mode="modeForm"
          :modalBoxShow="modalBoxShow"
          :employeeId="employeeId"
          v-on:hideModalBox="hideModalBox()"
          :popUpShow="popUpShow"
          v-on:exitModalBox="exitModalBox()"
          v-on:warningSave="warningSave()"
        />
      </div>
    </div>
    <div class="paging-bar">
      <div class="paging-bar-note-left">Hiển thị 1-10/1000 nhân viên</div>
      <div class="paging-bar-note-right">10 nhân viên/trang</div>
      <div class="paging-bar-btn">
        <div class="paging-bar-btn-first-page">
          <img src="../../assets/icon/btn-firstpage.svg" />
        </div>
        <div class="paging-bar-btn-prev-page">
          <img src="../../assets/icon/btn-prev-page.svg" />
        </div>
        <div class="page-number-one">1</div>
        <div class="paging-bar-btn-page-number">2</div>
        <div class="paging-bar-btn-page-number">3</div>
        <div class="paging-bar-btn-page-number">4</div>
        <div class="paging-bar-btn-next-page">
          <img src="../../assets/icon/btn-next-page.svg" />
        </div>
        <div class="paging-bar-btn-last-page">
          <img src="../../assets/icon/btn-lastpage.svg" />
        </div>
      </div>
      <Popup
        :type="modePopup"
        :showPopup="popUpShow"
        v-on:hidePopup="hidePopup($event)"
      />
    </div>
  </div>

  <!-- </div> -->
</template>
<script>
import axios from "axios";
import ModalBox from "../ModalBox/TheModal.vue";
import Combobox from "../base/BaseComboBox.vue";
import Popup from "../base/BasePopup.vue";
// import VueAxios from 'vue-axios';
export default {
  name: "Content",
  components: {
    ModalBox,
    Combobox,
    Popup,
  },
  props: {
    msg: String,
  },
  mounted() {
    var vm = this;
    axios
      .get("http://cukcuk.manhnv.net/v1/Employees")
      .then((res) => {
        console.log(res);
        vm.employee = res.data;
      })
      .catch((res) => {
        console.log(res);
      });
  },
  data() {
    return {
      isDelete: false,
      btnDelete: false,
      deleteQueue: [],
      modalIsSave: false,
      employee: [],
      employeeId: "",
      modalBoxShow: false,
      popUpShow: false,
      modeForm: 0,
      modePopup: 0,
      department: "",
      position: "",
      dataComboboxDepartment: {
        Id: this.department,
        Name: "",
      },
      dataComboboxPosition: {
        Id: this.position,
        Name: "",
      },
    };
  },
  methods: {
    /**
     * Xu ly su kien double click vao mot hang trong bang thong tin nhan vien
     */
    dbClickHandle(employeeId) {
      this.modalBoxShow = !this.modalBoxShow;
      this.employeeId = employeeId;
      this.modeForm = 1; //che do sua thong tin nhan vien
      console.log(this.employeeId);
      console.log(this.employee);
    },
    tdClickHandle(e, employeeId) {
      this.btnDelete = true;
      console.log(employeeId);
      e.currentTarget.classList.toggle("table-checkbox-default");
      e.currentTarget.classList.toggle("table-checkbox--active");
      var index = this.deleteQueue.indexOf(employeeId);
      if (e.currentTarget.children[0].children[0].checked) {
        //console.log(e.currentTarget.children[0].children[0].checked);
        e.currentTarget.children[0].children[0].checked = false;
      } else {
        //console.log(e.currentTarget.children[0].children[0].checked);
        e.currentTarget.children[0].children[0].checked = true;
      }
      if (index == -1) {
        this.deleteQueue.push(employeeId);
      } else {
        this.deleteQueue.splice(index, 1);
        if (this.deleteQueue.length == 0) {
          this.btnDelete = false;
        }
      }
      console.log(this.btnDelete);
    },
    async btnDeleteClick() {
      await this.changeStatePopup();
      this.modePopup = 1;
    },
    deleteMul() {
      this.deleteQueue.forEach((item) => {
        axios
          .delete(`http://cukcuk.manhnv.net/v1/employees/${item}`)
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.error(err);
          });
      });
    },
    /**
     * Lay du lieu ve phong ban
     */
    getDepartment(value, name) {
      console.log(value);
      this.department = value;
      this.dataComboboxDepartment.Name = name;
    },
    /**
     * Lay du lieu ve vi tri
     */
    getPosition(value, name) {
      console.log(value);
      this.position = value;
      this.dataComboboxPosition.Name = name;
    },
    showModalBox() {
      console.log("click");
      this.modalBoxShow = !this.modalBoxShow;
      this.modeForm = 0; //Che do them nhan vien moi vao danh sach
    },
    /**
     * Xu ly Popup khi muon dong ModalBox
     */
    async exitModalBox() {
      await this.changeStatePopup();
      this.modePopup = 0;
    },
    /**
     * Xu ly Popup khi muon xoa 1 ban ghi
     */
    async warningDelete() {
      await this.changeStatePopup();
      this.modePopup = 1;
    },
    /**
     * Xu ly Popup khi muon luu 1 ban ghi
     */
    async warningSave() {
      await this.changeStatePopup();
      this.modePopup = 2;
    },
    changeStatePopup() {
      this.popUpShow = !this.popUpShow;
      this.modalIsSave = false;
    },
    hideModalBox() {
      this.modalBoxShow = !this.modalBoxShow;
      this.modeForm = 2;
    },
    hidePopup(mode) {
      if (mode == 1) {
        // debugger;
        this.popUpShow = !this.popUpShow;
        this.isDelete = false;
      } else if (mode == 2) {
        debugger;
        this.modalIsSave = true;
        this.popUpShow = !this.popUpShow;
      } else if (mode == 3) {
        this.isDelete = true;
        this.popUpShow = !this.popUpShow;
        this.deleteMul();
      } else {
        this.popUpShow = !this.popUpShow;
        this.modalBoxShow = !this.modalBoxShow;
        this.modeForm = 2;
      }
    },
    formatDate(date) {
      if (date) {
        var rel = "";
        var word = date.split("-");
        for (var i = 0; i < 2; i++) {
          rel += word[2][i];
        }
        return (rel += "/" + word[1] + "/" + word[0]);
      } else {
        return "";
      }
    },
    formatSalary(money) {
      if (money) {
        var num = money.toFixed(0).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1.");
        return num;
      } else {
        console.log("Khong co luong");
        return "";
      }
    },
  },
  computed: {
    showBtnDelete() {
      if (this.btnDelete) {
        return "flex";
      } else {
        return "none";
      }
    },
  },
};
</script>
<style>
</style>