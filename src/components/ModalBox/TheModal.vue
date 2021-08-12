<template >
  <div>
    <div class="wrap" :style="{ display: modalBoxState }">
      <div class="box-infor">
        <div class="box-infor-header">
          <div class="header-title"><b>THÔNG TIN NHÂN VIÊN</b></div>
          <div class="header-exit-icon" id="exit " @click="changePopup()">
            <i class="fas fa-times"></i>
          </div>
        </div>
        <div class="box-infor-avatar">
          <div class="avatar-image"></div>
          <div class="avatar-note">
            <p>(Vui lòng chọn ảnh có định dạng</p>

            <p>.jpg, .jpeg, .png, .gif)</p>
          </div>
        </div>
        <div class="box-infor-content">
          <div class="content-private-infor">
            <div class="content-private-infor-title">
              <p>A. THÔNG TIN CHUNG:</p>
              <div class="line"></div>
            </div>
            <div class="title-row">
              <p class="col-1">Mã nhân viên(<span>*</span>)</p>
              <p class="col-2">Họ và tên(<span>*</span>)</p>
            </div>
            <div class="input-row">
              <input
                class="col-1 input"
                require
                type="text "
                id="textEmployeeCode"
                v-model="employee.EmployeeCode"
                autofocus
                v-on:blur="handleBlur"
                v-on:focus="handleFocus"
                v-bind:title="'Trường dữ liệu bắt buộc nhập'"
              />
              <input
                class="input"
                require
                type="text "
                id="textName"
                v-model="employee.FullName"
                v-on:blur="handleBlur"
                v-on:focus="handleFocus"
                v-bind:title="'Trường dữ liệu bắt buộc nhập'"
              />
            </div>
            <!-- Div ngay sinh, gioi tinh -->
            <div class="title-row">
              <p class="col-1">Ngày sinh</p>
              <p class="col-2">Giới tính</p>
            </div>
            <div class="input-row">
              <div class="calendar col-1">
                <div class="drop-down">
                  <div class="drop-down-box">
                    <input
                      type="date"
                      class="combo-box-input"
                      id="textDateOfBirth"
                      v-model="employee.DateOfBirth"
                    />
                    <!-- <div class="drop-down-icon">
                                        <i class="far fa-calendar "></i>
                                    </div> -->
                  </div>
                  <!-- <ul class="drop-down-list" for="dropdown-list">
                                    <li class="select">Phòng nhân sự</li>
                                    <li class="drop-down-item">Phòng hành chính</li>
                                    <li class="drop-down-item">Phòng công nghệ</li>
                                    <li class="drop-down-item">Phòng đào tạo</li>
                                </ul> -->
                </div>
              </div>
              <div class="calendar">
                <!-- <i class="fas fa-chevron-down "></i> -->
                <Combobox
                  :data="dataGender"
                  :type="'Gender'"
                  :dataCombobox="dataComboboxGender"
                  :mode="1"
                  v-on:gender="getGender"
                />
              </div>
            </div>
            <div class="title-row">
              <p class="col-1">Số CMTND/ Căn cước (<span>*</span>)</p>
              <p class="col-2">Ngày cấp</p>
            </div>
            <div class="input-row">
              <input
                class="col-1 input"
                require
                type="text "
                id="textIdentitesNumber"
                v-model="employee.IdentityNumber"
                v-on:blur="handleBlur"
                v-on:focus="handleFocus"
                v-bind:title="'Trường dữ liệu bắt buộc nhập'"
              />
              <div class="calendar day-supply">
                <div class="drop-down">
                  <div class="drop-down-box">
                    <input
                      type="date"
                      class="combo-box-input"
                      id="textIdentitesDate"
                      v-model="employee.IdentityDate"
                    />
                    <!-- <div class="drop-down-icon">
                                        <i class="far fa-calendar "></i>
                                    </div> -->
                  </div>
                  <!-- <ul class="drop-down-list" for="dropdown-list">
                                    <li class="select">Phòng nhân sự</li>
                                    <li class="drop-down-item">Phòng hành chính</li>
                                    <li class="drop-down-item">Phòng công nghệ</li>
                                    <li class="drop-down-item">Phòng đào tạo</li>
                                </ul> -->
                </div>
              </div>
            </div>
            <!-- Noi cap -->
            <div class="title-row">
              <p class="col-1">Nơi cấp</p>
            </div>
            <div class="input-row">
              <input
                class="col-1 input"
                type="text "
                value="TP Hà Nội "
                id="textIdentitiesPlace"
                v-model="employee.IndentityPlace"
              />
            </div>
            <!-- Thông tin lien lac -->
            <div class="title-row">
              <p class="col-1">Email (<span>*</span>)</p>
              <p class="col-2">Số điện thoại (<span>*</span>)</p>
            </div>
            <div class="input-row">
              <input
                class="col-1 input"
                require
                type="text "
                id="textEmail"
                v-model="employee.Email"
                v-on:blur="handleBlurEmail"
                v-on:focus="handleFocus"
                v-bind:title="'Trường dữ liệu bắt buộc nhập'"
              />
              <input
                class="input"
                require
                type="text "
                id="textPhoneNumber"
                v-model="employee.PhoneNumber"
                v-on:blur="handleBlur"
                v-on:focus="handleFocus"
                v-bind:title="'Trường dữ liệu bắt buộc nhập'"
              />
            </div>
          </div>
          <div class="content-job-infor">
            <div class="content-private-infor-title">
              <p>B. THÔNG TIN CÔNG VIỆC:</p>
              <div class="line"></div>
            </div>
            <!-- Vị trí công tác -->
            <div class="title-row">
              <p class="col-1">Vị trí</p>
              <p class="col-2">Phòng ban</p>
            </div>
            <div class="input-row">
              <div class="calendar col-1">
                <Combobox
                  :api="'http://cukcuk.manhnv.net/v1/Positions'"
                  :type="'Position'"
                  :dataCombobox="dataComboboxPosition"
                  :mode="1"
                  v-on:position="getPosition"
                />
              </div>
              <div class="department">
                <Combobox
                  :api="'http://cukcuk.manhnv.net/api/Department'"
                  :type="'Department'"
                  :dataCombobox="dataComboboxDepartment"
                  :mode="1"
                  v-on:department="getDepartment"
                />
              </div>
            </div>
            <!-- Thông tin thuế và lương -->
            <div class="title-row">
              <p class="col-1">Mã số thuế cá nhân</p>
              <p class="col-2">Mức lương cơ bản</p>
            </div>
            <div class="input-row salary-box">
              <input
                class="col-1 input"
                type="text "
                id="textTaxNumber"
                v-model="employee.PersonalTaxCode"
              />
              <div class="salary" id="salary">
                <input
                  class="col-2"
                  type="text"
                  id="textSalary"
                  name="amount"
                  v-model="employee.Salary"
                />
                <span>(VNĐ)</span>
              </div>
            </div>
            <!-- Ngày gia nhập công ty -->
            <div class="title-row">
              <p class="col-1">Ngày gia nhập công ty</p>
              <p class="col-2">Tình trạng công việc</p>
            </div>
            <div class="input-row">
              <div class="calendar col-1 day-in">
                <div class="drop-down">
                  <div class="drop-down-box">
                    <input
                      type="date"
                      class="combo-box-input"
                      id="textDayIn"
                      v-model="employee.JoinDate"
                    />
                    <!-- <div class="drop-down-icon ">
                                        <i class="far fa-calendar "></i>
                                    </div> -->
                  </div>
                  <!-- <ul class="drop-down-list " for="dropdown-list ">
                                    <li class="select ">Phòng nhân sự</li>
                                    <li class="drop-down-item ">Phòng hành chính</li>
                                    <li class="drop-down-item ">Phòng công nghệ</li>
                                    <li class="drop-down-item ">Phòng đào tạo</li>
                                </ul> -->
                </div>
              </div>
              <div class="calendar">
                <Combobox
                  :data="dataWorkStatus"
                  :type="'WorkStatus'"
                  :dataCombobox="dataComboboxWorkStatus"
                  :mode="1"
                  v-on:workstatus="getWorkStatus"
                />
              </div>
            </div>
          </div>
        </div>
        <div class="box-infor-footer">
          <div class="box-infor-footer-btn">
            <div
              class="box-infor-footer-btn-delete"
              v-if="mode == 1"
              @click="deleteEmployee()"
            >
              <i class="far fa-trash-alt"></i>
              <p>Xóa</p>
            </div>
            <div class="box-infor-footer-btn-cancel" @click="changePopup()">
              <p>Hủy</p>
            </div>
            <div
              class="box-infor-footer-btn-save button"
              id="btn-save"
              @click="changePopupSave()"
            >
              <i class="far fa-save"></i>
              <div class="box-infor-footer-btn-save-text">
                <p>Lưu</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import moment from "moment";
import axios from "axios";
import Combobox from "../base/BaseComboBox.vue";
export default {
  name: "ModalBox",
  components: {
    Combobox,
  },
  props: {
    //Bien tat/bat form thong tin chi tiet
    modalBoxShow: Boolean,
    // Ma Id cua nhan vien
    employeeId: {
      type: String,
      default: "",
      require: true,
    },
    // Che do hien thi ung voi them moi nhan vien hay chinh sua thong tin
    mode: {
      type: Number,
      default: 0, //0 ung voi them moi, 1 ung voi sua
      require: true,
    },
    popUpShow: {
      type: Boolean,
    },
    isSave: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      IsSave: this.isSave,
      formMode: this.mode,
      show: true,
      employee: {},
      dataGender: [
        { GenderName: "Nữ", GenderId: 0 },
        { GenderName: "Nam", GenderId: 1 },
        { GenderName: "Không xác định", GenderId: 2 },
      ],
      dataWorkStatus: [
        { WorkStatusId: 1, WorkStatusName: "Thực tập" },
        { WorkStatusId: 2, WorkStatusName: "Thử việc" },
        { WorkStatusId: 3, WorkStatusName: "Đã nghỉ" },
        { WorkStatusId: 4, WorkStatusName: "Chính thức" },
      ],
      requireAlert: false,
      isNull: true,
      gender: "",
      department: "",
      position: "",
      workstatus: "",
      dataComboboxDepartment: {
        Id: this.department,
        Name: "",
      },
      dataComboboxPosition: {
        Id: this.position,
        Name: "",
      },
      dataComboboxGender: {
        Id: this.gender,
        Name: "",
      },
      dataComboboxWorkStatus: {
        Id: this.workstatus,
        Name: "",
      },
    };
  },
  computed: {
    modalBoxState() {
      if (this.modalBoxShow) {
        return "flex";
      } else {
        return "none";
      }
    },
  },
  methods: {
    /**
     * Dong ModalBox
     */
    changePopup() {
      this.$emit("exitModalBox");
      // this.$emit('tableUpdated');
    },
    changePopupSave() {
      this.$emit("warningSave");
      // this.$emit('tableUpdated');
    },
    changePopupDelete() {
      this.$emit("warningDelete");
      // this.$emit('tableUpdated');
    },
    /**
     * Thay đổi trạng thái ẩn/hiện của modalBox
     */
    changeState() {
      this.$emit("hideModalBox");
      this.requireAlert = false;
    },
    /**
     * Format du lieu ngay thang nam khi day vao form modal
     */
    formatDateForm(date) {
      if (date) {
        return moment(String(date)).format("YYYY-MM-DD");
      } else {
        return "";
      }
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
    /**
     * Lay du lieu ve gioi tinh
     */
    getGender(value, name) {
      console.log(value);
      this.gender = value;
      this.dataComboboxGender.Name = name;
    },
    /**
     * Lay du lieu ve tinh trang cong viec
     */
    getWorkStatus(value, name) {
      console.log(value);
      this.workstatus = value;
      this.dataComboboxWorkStatus.Name = name;
    },
    /**
     * Kiem tra cac truong bat buoc nhap truoc khi save
     */
    validateData() {
      // debugger;
      if (
        this.employee.FullName &&
        this.employee.EmployeeCode &&
        this.employee.Email &&
        this.employee.PhoneNumber
      ) {
        this.isNull = false;
      } else {
        this.isNull = true;
        alert("Chưa nhập những trường dữ liệu bắt buộc");
      }
    },
    /**
     * Kiem tra hop le cua email
     */
    validateEmail() {
      const re =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(String(this.employee.Email).toLowerCase());
    },
    /**
     * Xu ly su kien blur tren cac input bat buoc
     */
    handleBlur(e) {
      if (e.target.value == "") {
        this.requireAlert = true;
      } else {
        this.requireAlert = false;
      }

      if (this.requireAlert == true) {
        e.target.style.border = "1px solid #FF4747";
      } else {
        e.target.style.border = "1px solid #bbbbbb";
      }
    },
    /**
     * Xu ly su kien blur cua Input Email
     */
    handleBlurEmail(e) {
      if (e.target.value == "" || !this.validateEmail()) {
        this.requireAlert = true;
      } else {
        this.requireAlert = false;
      }

      if (this.requireAlert == true) {
        e.target.style.border = "1px solid #FF4747";
      } else {
        e.target.style.border = "1px solid #bbbbbb";
      }
    },
    /**
     * Xu ly su kien focus cua cac input bat buoc de chen len border alert
     */
    handleFocus(e) {
      e.target.style.border = "1px solid #019160";
    },
    /**
     * Them/sua nhan vien
     */
    saveEditEmployee() {
      //this.validateData();
      let vm = this;
      this.validateData();
      if (!this.isNull && this.validateEmail()) {
        if (vm.mode == 0) {
          vm.employee.DepartmentId = vm.department;
          vm.employee.PositionId = vm.position;
          vm.employee.Gender = vm.gender;
          vm.employee.WorkStatus = vm.workstatus;
          axios
            .post(`http://cukcuk.manhnv.net/v1/employees`, vm.employee)
            .then((res) => {
              console.log(res);
              vm.$emit("refreshTable");
              debugger;

              //alert("Lưu thành công");
              //debugger;
            })
            .catch((err) => {
              console.error(err);
            });
          vm.changeState();
        } else if (vm.mode == 1) {
          vm.employee.DepartmentId = vm.department;
          vm.employee.PositionId = vm.position;
          vm.employee.Gender = vm.gender;
          vm.employee.WorkStatus = vm.workstatus;
          axios
            .put(
              `http://cukcuk.manhnv.net/v1/employees/${vm.employeeId}`,
              vm.employee
            )
            .then((res) => {
              console.log(res);
              this.$emit("refreshTable");
              alert("Sửa thành công");
            })
            .then(() => {
              vm.changeState();
            })
            .catch((err) => {
              console.error(err);
            });
        }
      } else if (!this.validateEmail()) {
        alert("Nhap lai email theo dung dinh dang");
      }
    },
    deleteEmployee() {
      let vm = this;
      vm.employee.DepartmentId = vm.department;
      vm.employee.PositionId = vm.position;
      vm.employee.Gender = vm.gender;
      axios
        .delete(
          `http://cukcuk.manhnv.net/v1/employees/${vm.employeeId}`,
          vm.employee
        )
        .then((res) => {
          console.log(res);
          vm.changeState();
          this.$emit("refreshTable");
        })
        .catch((err) => {
          console.error(err);
        });
    },
    getNewEmployeeCode() {
      axios
        .get("http://cukcuk.manhnv.net/v1/Employees/NewEmployeeCode")
        .then((res) => {
          this.employee.EmployeeCode = res.data;
          console.log(res.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  watch: {
    employee: function () {
      console.log(this.employee);

      var dob = this.employee.DateOfBirth;
      this.employee.DateOfBirth = this.formatDateForm(dob);
      console.log(this.employee.DateOfBirth);

      var IndentityDate = this.employee.IdentityDate;
      this.employee.IdentityDate = this.formatDateForm(IndentityDate);
      console.log(this.employee.IdentityDate);

      var dayIn = this.employee.JoinDate;
      this.employee.JoinDate = this.formatDateForm(dayIn);
    },
    employeeId: function (value) {
      //Neu ma Id cua nhan vien thay doi thi thuc hien lay lai du lieu moi

      let vm = this;
      axios
        .get(`http://cukcuk.manhnv.net/v1/employees/${value}`)
        .then((res) => {
          vm.employee = res.data;
          vm.dataComboboxPosition.Name = vm.employee.PositionName;
          vm.position = res.data.PositionId;
          vm.dataComboboxGender.Name = vm.employee.GenderName;
          vm.gender = vm.employee.Gender;
          vm.dataWorkStatus.forEach((element) => {
            if (element.WorkStatusId == vm.employee.WorkStatus) {
              vm.dataComboboxWorkStatus.Name = element.WorkStatusName;
            }
          });
          vm.workstatus = vm.employee.WorkStatus;
        })
        .catch((err) => {
          console.error(err);
        });
    },
    mode: function () {
      //Neu la them moi nhan vien thi don toan bo du lieu trong form thong tin chi tiet
      debugger;
      if (this.mode == 0) {
        debugger;
        this.employee = {};
        debugger;
        axios
          .get("http://cukcuk.manhnv.net/v1/Employees/NewEmployeeCode")
          .then((res) => {
            debugger;
            //this.employee.EmployeeCode = res.data;
            this.$set(this.employee, "EmployeeCode", res.data);
            console.log(this.employee.EmployeeCode);
          })
          .catch((err) => {
            console.log(err);
          });
      }
    },
    isSave: function () {
      if (this.isSave) {
        // debugger;
        this.saveEditEmployee();
      }
    },
  },
};
</script>
<style lang="">
</style>