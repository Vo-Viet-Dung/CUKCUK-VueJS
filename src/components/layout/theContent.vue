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
            <div class="content-add-employee-button">
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
                <tbody><tr employeeid="28a65d40-ef90-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-864</td>
     <td></td>
     <td>Nữ</td>
     <td class="align-center">01/01/1970</td>
     <td></td>
     <td title="sadjdksal@gmail.com">sadjdksal@gmail.com</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right"></td>
     <td></td>
 </tr><tr employeeid="005d0185-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-368</td>
     <td>Nguyễn Thủy Long</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0265353692</td>
     <td title="nhanvien.MF368@misa.cukcuk.vn">nhanvien.MF368@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng Công nghệ</td>
     <td class="align-right">436.277.164</td>
     <td>2</td>
 </tr><tr employeeid="0083a557-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-25</td>
     <td>Lưu Việt Đức</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0305205933</td>
     <td title="nhanvien.MF25@misa.cukcuk.vn">nhanvien.MF25@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng Nhân sự</td>
     <td class="align-right">974.034.273</td>
     <td>1</td>
 </tr><tr employeeid="00845303-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-380</td>
     <td>Nguyễn Văn Hường</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0599229786</td>
     <td title="nhanvien.MF380@misa.cukcuk.vn">nhanvien.MF380@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">712.468.823</td>
     <td>3</td>
 </tr><tr employeeid="0084b005-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-382</td>
     <td>Mạc Đức Tú</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0330264449</td>
     <td title="nhanvien.MF382@misa.cukcuk.vn">nhanvien.MF382@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng Marketting</td>
     <td class="align-right">92.757.645</td>
     <td>1</td>
 </tr><tr employeeid="0085735b-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-383</td>
     <td>Mạc Việt Loan</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0585249332</td>
     <td title="nhanvien.MF383@misa.cukcuk.vn">nhanvien.MF383@misa.cukcuk.vn</td>
     <td title="Nhân" viên="">Nhân viên</td>
     <td>Phòng Nhân sự</td>
     <td class="align-right">654.554.815</td>
     <td>3</td>
 </tr><tr employeeid="008f0834-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-384</td>
     <td>Lý Thị Trâm</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0972641564</td>
     <td title="nhanvien.MF384@misa.cukcuk.vn">nhanvien.MF384@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">211.480.059</td>
     <td>2</td>
 </tr><tr employeeid="008ff029-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-385</td>
     <td>Đỗ Việt Dũng</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0585324580</td>
     <td title="nhanvien.MF385@misa.cukcuk.vn">nhanvien.MF385@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">284.663.470</td>
     <td>4</td>
 </tr><tr employeeid="00906970-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-386</td>
     <td>Lê Hữu Khánh Ngọc</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0960542821</td>
     <td title="nhanvien.MF386@misa.cukcuk.vn">nhanvien.MF386@misa.cukcuk.vn</td>
     <td title="Phó" phòng="">Phó phòng</td>
     <td>Phòng Marketting</td>
     <td class="align-right">5.791.425</td>
     <td>1</td>
 </tr><tr employeeid="0090df76-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-27</td>
     <td>Lương Tiến Đức</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0912174466</td>
     <td title="nhanvien.MF27@misa.cukcuk.vn">nhanvien.MF27@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">43.243.108</td>
     <td>4</td>
 </tr><tr employeeid="0091b828-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-387</td>
     <td>Trần Thu Dũng</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0525573272</td>
     <td title="nhanvien.MF387@misa.cukcuk.vn">nhanvien.MF387@misa.cukcuk.vn</td>
     <td title="Nhân" viên="">Nhân viên</td>
     <td>Phòng Marketting</td>
     <td class="align-right">844.813.738</td>
     <td>4</td>
 </tr><tr employeeid="0092f8a3-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-388</td>
     <td>Lý Văn Hường</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0226363985</td>
     <td title="nhanvien.MF388@misa.cukcuk.vn">nhanvien.MF388@misa.cukcuk.vn</td>
     <td title="Phó" phòng="">Phó phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">357.904.694</td>
     <td>2</td>
 </tr><tr employeeid="009a88b8-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-389</td>
     <td>Trần Thị Trâm</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0545790217</td>
     <td title="nhanvien.MF389@misa.cukcuk.vn">nhanvien.MF389@misa.cukcuk.vn</td>
     <td title="Nhân" viên="">Nhân viên</td>
     <td>Phòng Marketting</td>
     <td class="align-right">374.115.077</td>
     <td>3</td>
 </tr><tr employeeid="009baa67-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-390</td>
     <td>Đậu Thị Trâm</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0139480855</td>
     <td title="nhanvien.MF390@misa.cukcuk.vn">nhanvien.MF390@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">364.630.704</td>
     <td>2</td>
 </tr><tr employeeid="009cd682-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-391</td>
     <td>Lưu Văn Hưng</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0273089708</td>
     <td title="nhanvien.MF391@misa.cukcuk.vn">nhanvien.MF391@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">523.421.349</td>
     <td>4</td>
 </tr><tr employeeid="009d7564-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-392</td>
     <td>Trương Thị Hùng</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0809280562</td>
     <td title="nhanvien.MF392@misa.cukcuk.vn">nhanvien.MF392@misa.cukcuk.vn</td>
     <td title="Nhân" viên="">Nhân viên</td>
     <td>Phòng Marketting</td>
     <td class="align-right">744.850.534</td>
     <td>4</td>
 </tr><tr employeeid="00a108d3-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-393</td>
     <td>Lê Hữu Khánh Lan</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0749302621</td>
     <td title="nhanvien.MF393@misa.cukcuk.vn">nhanvien.MF393@misa.cukcuk.vn</td>
     <td title="Nhân" viên="">Nhân viên</td>
     <td>Phòng Nhân sự</td>
     <td class="align-right">508.110.609</td>
     <td></td>
 </tr><tr employeeid="00a5f7a9-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-394</td>
     <td>Phạm Thủy Trâm</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0257885778</td>
     <td title="nhanvien.MF394@misa.cukcuk.vn">nhanvien.MF394@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">860.014.396</td>
     <td>1</td>
 </tr><tr employeeid="00b3ef46-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-400</td>
     <td>Đỗ Việt Tùng</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0285847609</td>
     <td title="nhanvien.MF400@misa.cukcuk.vn">nhanvien.MF400@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Công nghệ</td>
     <td class="align-right">541.585.723</td>
     <td>2</td>
 </tr><tr employeeid="00b77d1d-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-401</td>
     <td>Lưu Việt Tú</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0226085439</td>
     <td title="nhanvien.MF401@misa.cukcuk.vn">nhanvien.MF401@misa.cukcuk.vn</td>
     <td title="Phó" phòng="">Phó phòng</td>
     <td>Phòng Marketting</td>
     <td class="align-right">242.890.903</td>
     <td>1</td>
 </tr><tr employeeid="00b7cf30-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-403</td>
     <td>Lương Ngọc Tú</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0270975814</td>
     <td title="nhanvien.MF403@misa.cukcuk.vn">nhanvien.MF403@misa.cukcuk.vn</td>
     <td title="Phó" phòng="">Phó phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">112.491.929</td>
     <td>1</td>
 </tr><tr employeeid="00b7fa48-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-402</td>
     <td>Võ Thủy Loan</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0454712033</td>
     <td title="nhanvien.MF402@misa.cukcuk.vn">nhanvien.MF402@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">233.527.386</td>
     <td>3</td>
 </tr><tr employeeid="0001ca04-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-337</td>
     <td>Lê Hữu Thu Long</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0853114237</td>
     <td title="nhanvien.MF337@misa.cukcuk.vn">nhanvien.MF337@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng Nhân sự</td>
     <td class="align-right">355.432.312</td>
     <td>3</td>
 </tr><tr employeeid="000315f7-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-338</td>
     <td>Lý Việt Mạnh</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0184612121</td>
     <td title="nhanvien.MF338@misa.cukcuk.vn">nhanvien.MF338@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Công nghệ</td>
     <td class="align-right">510.135.147</td>
     <td>2</td>
 </tr><tr employeeid="0006922c-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-339</td>
     <td>Lê Hữu Việt Đức</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>05855232</td>
     <td title="nhanvien.MF339@misa.cukcuk.vn">nhanvien.MF339@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">419.457.644</td>
     <td>4</td>
 </tr><tr employeeid="000712fa-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-13</td>
     <td>Văn Thu Loan</td>
     <td>Nam</td>
     <td class="align-center">08/01/2000</td>
     <td>0677736415</td>
     <td title="nhanvien.MF13@misa.cukcuk.vn">nhanvien.MF13@misa.cukcuk.vn</td>
     <td title="Phó" phòng="">Phó phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">560.876.610</td>
     <td>3</td>
 </tr><tr employeeid="000d73dd-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-341</td>
     <td>Trương Văn Loan</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0124652191</td>
     <td title="nhanvien.MF341@misa.cukcuk.vn">nhanvien.MF341@misa.cukcuk.vn</td>
     <td title="Giám" đốc="">Giám đốc</td>
     <td>Phòng Marketting</td>
     <td class="align-right">850.410.245</td>
     <td>1</td>
 </tr><tr employeeid="00146ca8-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-342</td>
     <td>Lưu Văn Hùng</td>
     <td></td>
     <td class="align-center">08/01/2000</td>
     <td>0837838925</td>
     <td title="nhanvien.MF342@misa.cukcuk.vn">nhanvien.MF342@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng Marketting</td>
     <td class="align-right">456.917.726</td>
     <td>2</td>
 </tr><tr employeeid="0015631a-ed5a-11eb-94eb-42010a8c0002">
    <td class="table-checkbox"><input type="checkbox"></td>
    <td>1</td>
     <td>NV-344</td>
     <td>Hồ Ngọc Tú</td>
     <td>Không xác định</td>
     <td class="align-center">08/01/2000</td>
     <td>0517897627</td>
     <td title="nhanvien.MF344@misa.cukcuk.vn">nhanvien.MF344@misa.cukcuk.vn</td>
     <td title="Trưởng" phòng="">Trưởng phòng</td>
     <td>Phòng đào tạo</td>
     <td class="align-right">208.335.356</td>
     <td>2</td>
 </tr></tbody>
                <!-- </table>
            </div>
            <div class="grid-body ">
                <table border="1px solid #000 " cellspacing="0 "> -->
                <tbody>
                </tbody>
            </table>
            <!-- </div> -->

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
export default {
     name: 'Content',
  props: {
    msg: String
  }
}
</script>
<style>
    
</style>