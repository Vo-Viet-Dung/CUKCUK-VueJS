<template >
    <div>
        <div class="wrap ">
            <div class="box-infor ">
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
                        <input class="col-1 input " require type="text " id="textEmployeeCode">
                        <input class="input " require type="text " id="textName">
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
                                    <input type="date" class="combo-box-input" id="textDateOfBirth">
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
                                    <input type="text" class="combo-box-input" id="textGender">
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
                        <input class="col-1 input " require type="text " value="1234567890 " id="textIdentitesNumber">
                        <div class="calendar day-supply">
                            <div class="drop-down">
                                <div class="drop-down-box">
                                    <input type="date" class="combo-box-input" id="textIdentitesDate">
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
                        <input class="col-1 input" type="text " value="TP Hà Nội " id="textIdentitiesPlace">
                    </div>
                    <!-- Thông tin lien lac -->
                    <div class="title-row ">
                        <p class="col-1 ">Email (<span>*</span>)</p>
                        <p class="col-2">Số điện thoại (<span>*</span>)</p>
                    </div>
                    <div class="input-row ">
                        <input class="col-1 input " require type="text " value="dungvv117@gmail.com" id="textEmail">
                        <input class="input" require type="text " value="0123456789 " id="textPhoneNumber">
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
                                    <input type="text" class="combo-box-input" id="textWorkspace-form">
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
                        <input class="col-1 input" type="text " id="textTaxNumber">
                        <div class="salary" id="salary">
                            <input class="col-2" type="text" id="textSalary" name="amount">
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
                                    <input type="date" class="combo-box-input " id="textDayIn">
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
                                    <input type="text " class="combo-box-input " id="textWorkStatus">
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
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'ContentModal',
  props: {
    msg: String
  }
}
</script>
<style lang="">
    
</style>