<template>
    <!-- <div> -->
        <div class="content">
        <div class="content-title">
            <div class="content-title-text">Danh sách nhân viên</div>
            <div class="content-delete-employee-button">
                <div class="content-delete-employee-button-icon">
                    <i class="far fa-trash-alt"></i>
                </div>
                <div class="content-delete-employee-button-text">Xóa nhân viên</div>
            </div>
            <div class="content-add-employee-button" @click="showModalBox()">
                <div class="content-add-employee-button-icon">
                    <img src="../../assets/icon/add.png" />
                </div>
                <div class="content-add-employee-button-text" id="open">Thêm nhân viên</div>
            </div>

        </div>
        <div class="content-option">
            <!-- <div class="content-option-search">
                <div class="content-option-search-icon"></div> -->
            <input class="content-option-search-text" placeholder="Tìm kiếm theo Mã, tên hoặc Số điện thoại">
            <!-- </div> -->
            <div class="content-option-workspace">
                <!-- <div class="content-option-workspace-text">Tất cả phòng ban</div>
                <div class="content-option-workspace-icon">
                    <i class="fas fa-chevron-down"></i>
                </div> -->
                <div class="drop-down">
                    <div class="drop-down-box">
                        <input type="text" class="combo-box-input" id="department-input" placeholder="Tất cả phòng ban">
                        <div class="drop-down-icon" id='workspace'>
                            <i class="fas fa-chevron-down " for="dropdown"></i>
                        </div>
                    </div>
                    <ul class="drop-down-list Workspace" for="dropdown-list">
                        <!-- <li class="select">Phòng nhân sự</li>
                        <li class="drop-down-item">Phòng hành chính</li>
                        <li class="drop-down-item">Phòng công nghệ</li>
                        <li class="drop-down-item">Phòng đào tạo</li> -->
                    </ul>
                </div>
            </div>
            <div class="content-option-position">
                <!-- <div class="content-option-position-text">Tất cả các vị trí</div>
                <div class="content-option-position-icon">
                    <i class="fas fa-chevron-down"></i>
                </div> -->
                <div class="drop-down-box">
                    <input type="text" class="combo-box-input" id="position-input" placeholder="Tất cả các vị trí">
                    <div class="drop-down-icon" id="position">
                        <i class="fas fa-chevron-down "></i>
                    </div>
                </div>
                <ul class="drop-down-list Position" for="dropdown-list">
                    <!-- <li class="select">Tổng giám đốc</li>
                    <li class="drop-down-item">Nhân viên</li>
                    <li class="drop-down-item">Fresher</li>
                    <li class="drop-down-item">Trưởng phòng</li> -->
                </ul>
            </div>
            <div class="content-option-reload">
                <!-- <img src="../../assets/icon/refresh.png" /> -->
            </div>
        </div>
        
        <div class="grid ">
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
                <tr  v-for="employee in employee" :key="employee.EmployeeId" @dblclick="dbClickHandle(employee.EmployeeId)">
                    <td class="table-checkbox"><input type="checkbox" ></td>
                    <td>1</td>
                    <td>{{employee.EmployeeCode}}</td>
                    <td>{{employee.FullName}}</td>
                    <td>{{employee.GenderName}}</td>
                    <td class="align-center">{{formatDate(employee.DateOfBirth)}}</td>
                    <td>{{employee.PhoneNumber}}</td>
                    <td >{{employee.Email}}</td>
                    <td >{{employee.PositionName}}</td>
                    <td>{{employee.DepartmentName}}</td>
                    <td class="align-right">{{formatSalary(employee.Salary)}}</td>
                    <td>{{employee.WorkStatus}}</td>
                </tr>
                </tbody>
            </table>
            <!-- </div> -->
        <div>
         <ModalBox :mode="modeForm" :modalBoxShow="modalBoxShow" :employeeId="employeeId" v-on:hideModalBox="hideModalBox()" />
        </div>
        </div>
        <div class="paging-bar ">
            <div class="paging-bar-note-left ">Hiển thị 1-10/1000 nhân viên</div>
            <div class="paging-bar-note-right ">10 nhân viên/trang</div>
            <div class="paging-bar-btn ">
                <div class="paging-bar-btn-first-page ">
                    <img src="../../assets/icon/btn-firstpage.svg" />
                </div>
                <div class="paging-bar-btn-prev-page ">
                    <img src="../../assets/icon/btn-prev-page.svg" />
                </div>
                <div class="page-number-one ">
                    1
                </div>
                <div class="paging-bar-btn-page-number ">
                    2
                </div>
                <div class="paging-bar-btn-page-number ">
                    3
                </div>
                <div class="paging-bar-btn-page-number ">
                    4
                </div>
                <div class="paging-bar-btn-next-page ">
                    <img src="../../assets/icon/btn-next-page.svg" />
                </div>
                <div class="paging-bar-btn-last-page ">
                    <img src="../../assets/icon/btn-lastpage.svg" />
                </div>
            </div>
        </div>
        
    </div>

    <!-- </div> -->
</template>
<script>
import axios from 'axios';
import ModalBox from '../ModalBox/TheModal.vue'
// import VueAxios from 'vue-axios';
export default {
    name: 'Content',
    components: {
        ModalBox,
    },
    props: {
        msg: String
    },
    mounted(){
        var vm = this;
        axios.get("http://cukcuk.manhnv.net/v1/Employees").then(res=> {
                console.log(res);
                vm.employee = res.data;

        }).catch(res=>{
            console.log(res);
        })
    },
    data(){
        return {
            employee: [],
            employeeId: '',
            modalBoxShow: false,
            modeForm: 0,
        };
    },
    methods:{
        /**
         * Xu ly su kien double click vao mot hang trong bang thong tin nhan vien
         */
        dbClickHandle(employeeId){
                this.modalBoxShow = !this.modalBoxShow;
                this.employeeId = employeeId;
                this.modeForm = 1; //che do sua thong tin nhan vien
                console.log(this.employeeId);

        },
        showModalBox(){
            console.log("click");
            this.modalBoxShow = !this.modalBoxShow;
            this.modeForm = 0; //Che do them nhan vien moi vao danh sach
        },
        hideModalBox(){
            this.modalBoxShow = !this.modalBoxShow;
        },
        formatDate(date){
            var rel = "";
            var word = date.split('-');
            for(var i = 0; i < 2;  i++){
                rel += word[2][i];
            }
            return rel+= '/' + word[1] + '/' + word[0];
        },
        formatSalary(money){
            if (Number.isNaN(money)) {
                console.log("Khong co luong");
                return "";
            } else {
                var num = money.toFixed(0).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1.");
                return num;
            }
        },
    }

};
</script>
<style>
    
</style>