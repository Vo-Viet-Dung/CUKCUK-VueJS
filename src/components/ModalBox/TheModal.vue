<template >
    <div>
           <div class="wrap " :style="{display: modalBoxState}">
        <div class="box-infor ">
            <div class="box-infor-header ">
                <div class="header-title "><b>THÔNG TIN NHÂN VIÊN</b></div>
                <div class="header-exit-icon " id="exit " @click="changeState()">
                    <i class="fas fa-times "></i>
                </div>
            </div>
            <div class="box-infor-avatar ">
                <div class="avatar-image ">
                </div>
                <div class="avatar-note ">
                    <p>(Vui lòng chọn ảnh có định dạng</p>

                    <p>.jpg, .jpeg, .png, .gif)</p>
                </div>
            </div>
            <div class="box-infor-content ">
                <div class="content-private-infor ">
                    <div class="content-private-infor-title ">
                        <p>A. THÔNG TIN CHUNG:</p>
                        <div class="line "></div>
                    </div>
                    <div class="title-row ">
                        <p class="col-1 ">Mã nhân viên(<span>*</span>)</p>
                        <p class="col-2">Họ và tên(<span>*</span>)</p>
                    </div>
                    <div class="input-row ">
                        <input class="col-1 input " require type="text " id="textEmployeeCode" v-model="employee.EmployeeCode">
                        <input class="input " require type="text " id="textName" v-model="employee.FullName">
                    </div>
                    <!-- Div ngay sinh, gioi tinh -->
                    <div class="title-row ">
                        <p class="col-1 ">Ngày sinh</p>
                        <p class="col-2">Giới tính</p>
                    </div>
                    <div class="input-row ">
                        <div class="calendar col-1 ">

                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="date" class="combo-box-input" id="textDateOfBirth" v-model="employee.DateOfBirth">
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
                        <div class="calendar ">

                            <!-- <i class="fas fa-chevron-down "></i> -->
                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="text" class="combo-box-input" id="textGender" v-model="employee.GenderName">
                                    <div class="drop-down-icon" id="sex">
                                        <i class="fas fa-chevron-down "></i>
                                    </div>
                                </div>
                                <ul class="drop-down-list Sex">
                                    <!-- <li id="selected" curVal="1" class="drop-down-item">Nam</li>
                                    <li curVal="2" class="drop-down-item">Nữ</li>
                                    <li curVal="3" class="drop-down-item">Không xác định</li> -->
                                </ul>
                            </div>
                        </div>
                    </div>
                    <div class="title-row ">
                        <p class="col-1 ">Số CMTND/ Căn cước (<span>*</span>)</p>
                        <p class="col-2">Ngày cấp</p>
                    </div>
                    <div class="input-row ">
                        <input class="col-1 input " require type="text " value="1234567890 " id="textIdentitesNumber" v-model="employee.IdentityNumber">
                        <div class="calendar day-supply">
                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="date" class="combo-box-input" id="textIdentitesDate" v-model="employee.IdentityDate">
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
                    <div class="title-row ">
                        <p class="col-1 ">Nơi cấp</p>
                    </div>
                    <div class="input-row ">
                        <input class="col-1 input" type="text " value="TP Hà Nội " id="textIdentitiesPlace" v-model="employee.IndentityPlace">
                    </div>
                    <!-- Thông tin lien lac -->
                    <div class="title-row ">
                        <p class="col-1 ">Email (<span>*</span>)</p>
                        <p class="col-2">Số điện thoại (<span>*</span>)</p>
                    </div>
                    <div class="input-row ">
                        <input class="col-1 input " require type="text " value="dungvv117@gmail.com" id="textEmail" v-model="employee.Email">
                        <input class="input" require type="text " value="0123456789 " id="textPhoneNumber" v-model="employee.PhoneNumber">
                    </div>
                </div>
                <div class="content-job-infor ">
                    <div class="content-private-infor-title ">
                        <p>B. THÔNG TIN CÔNG VIỆC:</p>
                        <div class="line "></div>
                    </div>
                    <!-- Vị trí công tác -->
                    <div class="title-row ">
                        <p class="col-1 ">Vị trí</p>
                        <p class="col-2">Phòng ban</p>
                    </div>
                    <div class="input-row ">
                        <div class="calendar col-1 ">
                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="text" class="combo-box-input" id="textPosition-form">
                                    <div class="drop-down-icon" id="position-form-icon">
                                        <i class="fas fa-chevron-down "></i>
                                    </div>
                                </div>
                                <ul class="drop-down-list Position-form">
                                    <!-- <li class="select">Tổng giám đốc</li>
                                    <li class="drop-down-item">Nhân viên</li>
                                    <li class="drop-down-item">Fresher</li>
                                    <li class="drop-down-item">Trưởng Phòng</li> -->
                                </ul>
                            </div>
                        </div>
                        <div class="department ">
                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="text" class="combo-box-input" id="textWorkspace-form" v-model="employee.DepartmentName">
                                    <div class="drop-down-icon" id="workspace-form-icon">
                                        <i class="fas fa-chevron-down " for="dropdown"></i>
                                    </div>
                                </div>
                                <ul class="drop-down-list Workspace-form">
                                    <!-- <li class="select">Phòng nhân sự</li>
                                    <li class="drop-down-item">Phòng hành chính</li>
                                    <li class="drop-down-item">Phòng công nghệ</li>
                                    <li class="drop-down-item">Phòng đào tạo</li> -->
                                </ul>
                            </div>
                        </div>
                    </div>
                    <!-- Thông tin thuế và lương -->
                    <div class="title-row ">
                        <p class="col-1 ">Mã số thuế cá nhân</p>
                        <p class="col-2">Mức lương cơ bản</p>
                    </div>
                    <div class="input-row salary-box ">
                        <input class="col-1 input" type="text " id="textTaxNumber" v-model="employee.PersonalTaxCode">
                        <div class="salary" id="salary">
                            <input class="col-2" type="text" id="textSalary" name="amount" v-model="employee.Salary">
                            <span>(VNĐ)</span>
                        </div>

                    </div>
                    <!-- Ngày gia nhập công ty -->
                    <div class="title-row ">
                        <p class="col-1 ">Ngày gia nhập công ty</p>
                        <p class="col-2 ">Tình trạng công việc</p>
                    </div>
                    <div class="input-row ">
                        <div class="calendar col-1 day-in ">
                            <div class="drop-down ">
                                <div class="drop-down-box ">
                                    <input type="date" class="combo-box-input " id="textDayIn" v-model="employee.JoinDate">
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
                        <div class="calendar ">
                            <div class="drop-down ">
                                <div class="drop-down-box ">
                                    <input type="text " class="combo-box-input " id="textWorkStatus" v-model="employee.WorkSatus">
                                    <div class="drop-down-icon " id="work-status-icon">
                                        <i class="fas fa-chevron-down " for="dropdown "></i>
                                    </div>
                                </div>
                                <ul class="drop-down-list WorkStatus " for="dropdown-list ">
                                    <li class="select ">Thử việc</li>
                                    <li class="drop-down-item ">Thực tập</li>
                                    <li class="drop-down-item ">Chính thức</li>
                                    <li class="drop-down-item ">Đã nghỉ</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="box-infor-footer ">
                <div class="box-infor-footer-btn ">
                    <div class="box-infor-footer-btn-cancel " @click="changeState()">
                        <p>
                            Hủy
                        </p>
                    </div>
                    <div class="box-infor-footer-btn-save button " id="btn-save" @click="saveEditEmployee()">
                        <i class="far fa-save "></i>
                        <div class="box-infor-footer-btn-save-text ">
                            <p>
                                Lưu
                            </p>
                        </div>
                    </div>
                    <div class="box-infor-footer-btn-delete ">
                        <i class="far fa-trash-alt"></i>
                        <p>
                            Xóa
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    </div>
</template>
<script>
import moment from 'moment';
import axios from 'axios';
export default {
    name: 'ModalBox',
  props: {
    //Bien tat/bat form thong tin chi tiet  
    modalBoxShow: Boolean,
    // Ma Id cua nhan vien
    employeeId:{
        type: String,
        default: '',
        require: true,
    },
    // Che do hien thi ung voi them moi nhan vien hay chinh sua thong tin
    mode:{
        type: Number,
        default: 0,  //0 ung voi them moi, 1 ung voi sua
        require: true,
    }
  },
  data(){
      return {
          show: true,
          employee: {},
          dataGender: [
              { GenderName: "Nữ"},
              {GenderName: "Nam"},
              {GenderName: "Không xác định"},
          ],
      };
  },
  computed: {
      modalBoxState(){
          if(this.modalBoxShow){
              return "flex";
          }else{
              return "none";
          }
      },
  },
  methods: {
      /**
       * Thay đổi trạng thái ẩn/hiện của modalBox
       */
      changeState(){
          this.$emit('hideModalBox');
      },
      formatDateForm(date){
            if (date) {
                return moment(String(date)).format('YYYY-MM-DD')
            }else{return "";}
        },
      saveEditEmployee(){
          let vm = this;
          if(vm.mode == 0){
              axios.post(`http://cukcuk.manhnv.net/v1/employees`, vm.employee)
              .then(res=>{
                  console.log(res)
                  vm.changeState();
              }).catch(err=>{
                  console.error(err);
              })
          }else{
              axios.put(`http://cukcuk.manhnv.net/v1/employees/${vm.employeeId}`, vm.employee)
              .then(res=>{
                  console.log(res);
                  vm.changeState();
              }).catch(err=>{
                  console.error(err);
              })
          }
      },
  },
  watch:{
      employee: function(){
        console.log(this.employee);

        var dob = this.employee.DateOfBirth;
        this.employee.DateOfBirth = this.formatDateForm(dob);
        console.log(this.employee.DateOfBirth);

        var IndentityDate = this.employee.IdentityDate;
        this.employee.IdentityDate = this.formatDateForm(IndentityDate);
        console.log(this.employee.IdentityDate);
      },
      employeeId:function(value){
          //Neu ma Id cua nhan vien thay doi thi thuc hien lay lai du lieu moi
          let vm = this;
          axios.get(`http://cukcuk.manhnv.net/v1/employees/${value}`)
          .then(res=>{
              vm.employee = res.data;
          })
          .catch(err =>{
              console.error(err);
          })
      },
      mode: function(){
          //Neu la them moi nhan vien thi don toan bo du lieu trong form thong tin chi tiet
          if(this.mode == 0){
              this.employee = {};
          }
      }
  }
};
</script>
<style lang="">
    
</style>