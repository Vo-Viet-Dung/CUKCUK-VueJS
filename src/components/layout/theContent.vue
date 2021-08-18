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
        @keyup.enter="getInputSearch($event)"
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

      <div class="content-option-reload" @click="refreshTable()">
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
        <tbody v-if="isRefresh">
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
          v-on:refreshTable="refreshTable()"
        />
      </div>
    </div>
    <div class="paging-bar">
      <div class="paging-bar-note-left">Hiển thị 1-10/1000 nhân viên</div>
      <div class="paging-bar-note-right">
        <div class="pagging-dropdown-icon">
          <i class="fas fa-chevron-down" @click="showPaggingBox()"></i>
        </div>

        <div class="pagging-box" v-if="showPagging">
          <div
            class="pagging-item"
            v-for="(item, index) in numberRecordInOnePage"
            :key="index"
            @click="getInforBtnPageNumber($event)"
          >
            <span>{{ item }}</span> nhân viên/trang
          </div>
        </div>
        {{ pageSize }} nhân viên/trang
      </div>
      <div class="paging-bar-btn">
        <div class="paging-bar-btn-first-page" @click="firstPage()">
          <img src="../../assets/icon/btn-firstpage.svg" />
        </div>
        <div class="paging-bar-btn-prev-page" @click="prevPage()">
          <img src="../../assets/icon/btn-prev-page.svg" />
        </div>

        <!-- <div class="page-number-one">1</div>
        <div class="paging-bar-btn-page-number">2</div>
        <div class="paging-bar-btn-page-number">3</div>
        <div class="paging-bar-btn-page-number">4</div> -->
        <div
          class="paging-bar-btn-page-number"
          :class="{ active: pageCurrent == page ? true : false }"
          v-for="page in pages"
          :key="page"
          @click="getValuePageNumber(page)"
        >
          {{ page }}
        </div>

        <div class="paging-bar-btn-next-page" @click="nextPage()">
          <img src="../../assets/icon/btn-next-page.svg" />
        </div>
        <div class="paging-bar-btn-last-page" @click="lastPage()">
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
    // var vm = this;
    // axios
    //   .get("http://cukcuk.manhnv.net/v1/Employees")
    //   .then((res) => {
    //     console.log(res);
    //     vm.employee = res.data;
    //   })
    //   .catch((res) => {
    //     console.log(res);
    //   });
    axios
      .get(
        `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=${this.pageSize}&pageNumber=${this.pageCurrent}&employeeCode=NV`
      )
      .then((res) => {
        this.employee = res.data.Data;
        this.totalpage = res.data.TotalPage;
        this.totalRecord = res.data.TotalRecord;
        let pageObject = this.paginate(
          this.totalRecord,
          this.pageCurrent,
          this.pageSize,
          this.maxPages,
          this.totalpage
        );
        this.startIndex = pageObject.startIndex + 1;
        this.endIndex = pageObject.endPage + 1;
        this.pages = pageObject.pages;
        console.log(this.employee);
        console.log(this.pages);
      })
      .catch((err) => {
        console.log(err);
      });
    this.pageCurrent = 1;
  },
  data() {
    return {
      showPagging: false,
      numberRecordInOnePage: [10, 20, 30, 50],
      pageSize: 10,
      pageCurrent: 1,
      totalpage: 0,
      totalRecord: 0,
      maxPages: 10,
      startIndex: 1,
      endIndex: 10,
      pages: [],
      searchText: "NV",
      isRefresh: true,
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
    /**
     * Xu ly su kien click vao tr trong table
     */
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
    /**
     * Xu ly su kien khi click btnDelete
     */
    async btnDeleteClick() {
      await this.changeStatePopup();
      this.modePopup = 1;
    },
    deleteMul() {
      this.deleteQueue.forEach((item) => {
        var index = this.deleteQueue.indexOf(item);
        axios
          .delete(`http://cukcuk.manhnv.net/v1/employees/${item}`)
          .then((res) => {
            console.log(res);
          })
          .then(() => {
            this.refreshTable();
          })
          .catch((err) => {
            console.error(err);
          });
        this.deleteQueue.splice(index, 1);
      });

      if (this.deleteQueue.length == 0) {
        this.btnDelete = false;
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
    /**
     * format tiền lương trước khi đẩy vào bảng
     */
    formatSalary(money) {
      if (money) {
        var num = money.toFixed(0).replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "$1.");
        return num;
      } else {
        console.log("Khong co luong");
        return "";
      }
    },
    showPaggingBox() {
      this.showPagging = !this.showPagging;
    },
    /**
     * Chuyen ve trang dau tien
     */
    firstPage() {
      this.pageCurrent = 1;
    },
    /**
     * Chuyen den trang cuoi cung
     */
    lastPage() {
      this.pageCurrent = this.totalpage;
      console.log(this.pageCurrent);
    },
    /**
     * Chuyen ve trang lien truoc
     */
    nextPage() {
      this.pageCurrent = this.pageCurrent + 1;
    },
    /**
     * chuyen ve trang lien sau
     */
    prevPage() {
      this.pageCurrent = this.pageCurrent - 1;
    },
    /**
     * Lay so thu tu cua trang hien tai
     */
    getValuePageNumber(current) {
      this.pageCurrent = current;
      console.log(this.pageCurrent);
    },
    /**
     * lay thong tin phan trang khi click vao btnPage
     */
    getInforBtnPageNumber(e) {
      let value = e.target.innerText;
      let finalValue = "";
      for (let i = 0; i < 2; i++) {
        finalValue += value[i];
      }
      this.showPagging = !this.showPagging;
      finalValue = parseInt(finalValue, 10);
      this.pageSize = finalValue;
      this.pageCurrent = 1;
    },
    //Xử lý tính toán phân trang ( tổng số bản ghi, trang hiện tại, hiển thị thanh footer)
    paginate(totalRecord, pageCurrent, pageSize, maxPages, totalPage) {
      if (pageCurrent < 1) {
        pageCurrent = 1;
      } else if (pageCurrent > totalPage) {
        pageCurrent = totalPage;
      }

      let startPage, endPage;
      // tổng số trang nhiều hơn tối đa => tính trang bắt đầu và trang kết thúc
      let maxPagesBeforeCurrentPage;
      let maxPagesAfterCurrentPage;
      if (totalPage <= maxPages) {
        // tổng số trang ít hơn tối đa để hiển thị tất cả các trang
        startPage = 1;
        endPage = totalPage;
        // tổng số trang nhiều hơn tối đa => tính trang bắt đầu và trang kết thúc
        maxPagesBeforeCurrentPage = Math.floor(totalPage / 2);
        maxPagesAfterCurrentPage = Math.ceil(totalPage / 2) - 1;
      } else {
        // tổng số trang nhiều hơn tối đa => tính trang bắt đầu và trang kết thúc
        maxPagesBeforeCurrentPage = Math.floor(maxPages / 2);
        maxPagesAfterCurrentPage = Math.ceil(maxPages / 2) - 1;
        if (pageCurrent <= maxPagesBeforeCurrentPage) {
          // trang hiện tại gần đầu
          startPage = 1;
          endPage = maxPages;
        } else if (pageCurrent + maxPagesAfterCurrentPage >= totalPage) {
          // trang hiện tại gần cuối
          startPage = totalPage - maxPages + 1;
          endPage = totalPage;
        } else {
          // trang hiện tại nằm ở vùng giữa
          startPage = pageCurrent - maxPagesBeforeCurrentPage;
          endPage = pageCurrent + maxPagesAfterCurrentPage;
        }
      }
      let pages = Array.from(Array(endPage + 1 - startPage).keys()).map(
        (i) => startPage + i
      );
      // tính chỉ số của bản ghi bắt đầu và kết thúc
      let startIndex = (pageCurrent - 1) * pageSize;
      let endIndex = Math.min(startIndex + pageSize - 1, totalRecord - 1);
      var obj = {
        totalRecord: totalRecord,
        pageCurent: pageCurrent,
        pageSize: pageSize,
        totalPage: totalPage,
        startPage: startPage,
        endPage: endPage,
        startIndex: startIndex,
        endIndex: endIndex,
        pages: pages,
      };
      return obj;
    },
    /**
     * Lay API Phan trang
     */
    pagingProcessData(pageSize, pageCurrent) {
      this.isRefresh = !this.isRefresh;
      this.employee = {};
      axios
        .get(
          `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=${pageSize}&pageNumber=${pageCurrent}&employeeCode=NV`
        )
        .then((res) => {
          this.employee = res.data.Data;
          this.totalpage = res.data.TotalPage;
          this.totalRecord = res.data.TotalRecord;
          let pageObject = this.paginate(
            this.totalRecord,
            this.pageCurrent,
            this.pageSize,
            this.maxPages,
            this.totalpage
          );
          this.startIndex = pageObject.startIndex + 1;
          this.endIndex = pageObject.endPage + 1;
          this.pages = pageObject.pages;
          this.isRefresh = !this.isRefresh;
          console.log(this.pages);
        })
        .catch((err) => {
          console.log(err);
        });
    },

    /**
     * Load lại table
     */
    refreshTable() {
      this.pageSize = 10;
      this.pageCurrent = 1;
      this.isRefresh = !this.isRefresh;
      this.employee = {};
      axios
        .get(
          `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=${this.pageSize}&pageNumber=${this.pageCurrent}&employeeCode=NV`
        )
        .then((res) => {
          this.employee = res.data.Data;
          this.totalpage = res.data.TotalPage;
          this.totalRecord = res.data.TotalRecord;
          let pageObject = this.paginate(
            this.totalRecord,
            this.pageCurrent,
            this.pageSize,
            this.maxPages,
            this.totalpage
          );
          this.startIndex = pageObject.startIndex + 1;
          this.endIndex = pageObject.endPage + 1;
          this.pages = pageObject.pages;
          this.isRefresh = !this.isRefresh;
          console.log(this.pages);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    /**
     * Refresh lại danh sách khi thực hiện filter
     */
    refreshFilter(api) {
      this.isRefresh = !this.isRefresh;
      console.log(api);
      let vm = this;
      vm.employee = {};
      // if (this.deleteQueue.length == 0) {
      //   this.btnDelete = false;
      // }
      axios
        .get(api)
        .then((res) => {
          vm.employee = res.data.Data;
          this.isRefresh = !this.isRefresh;
          console.log(vm.employee);
          //this.showTable = !this.showTable;
        })
        .catch((err) => {
          console.error(err);
        });
    },
    getInputSearch(e) {
      this.searchText = e.target.value;
    },
    /**
     * Thực hiện Filter trong form danh sách nhân viên
     */
    filters() {
      // if (this.department && !this.position) {
      //   this.refreshFilter(
      //     `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=100&pageNumber=1&employeeCode=NV&departmentId=${this.department}`
      //   );
      // } else if (this.position && !this.department) {
      //   this.refreshFilter(
      //     `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=100&pageNumber=1&employeeCode=NV&positionId=${this.position}`
      //   );
      // } else if (!this.department && !this.position) {
      //   this.refreshTable();
      // } else if (this.department && this.position) {
      //   this.refreshFilter(
      //     `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=100&pageNumber=1&employeeCode=NV&departmentId=${this.department}&positionId=${this.position}`
      //   );
      // }
      this.refreshFilter(
        `http://cukcuk.manhnv.net/v1/Employees/Filter?pageSize=${this.pageSize}&pageNumber=${this.pageCurrent}&employeeCode=${this.searchText}&departmentId=${this.department}&positionId=${this.position}`
      );
      console.log(this.pageCurrent);
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
    // showPaggingBox() {
    //   if (this.showPagging) {
    //     return "block";
    //   } else {
    //     return "none";
    //   }
    // },
  },
  watch: {
    position: function () {
      this.filters();
    },
    department: function () {
      this.filters();
    },
    searchText: function () {
      if (!this.searchText) {
        this.searchText = "NV";
      }
      this.filters();
    },
    pageCurrent: function () {
      if (this.pageCurrent > this.totalpage) {
        this.pageCurrent = this.totalpage;
      } else if (this.pageCurrent < 1) {
        this.pageCurrent = 1;
      }
      this.pagingProcessData(this.pageSize, this.pageCurrent);
    },
    pageSize: function () {
      this.pagingProcessData(this.pageSize, this.pageCurrent);
    },
  },
};
</script>
<style>
</style>