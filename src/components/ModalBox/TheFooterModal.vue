<template >
    <div>
        <div class="wrap ">
            <div class="box-infor ">
                <div class="box-infor-footer ">
                <div class="box-infor-footer-btn ">
                    <div class="box-infor-footer-btn-cancel ">
                        <p>
                            Hủy
                        </p>
                    </div>
                    <div class="box-infor-footer-btn-save button ">
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
export default {
    name: 'FooterModal',
  props: {
    msg: String
  }
}
</script>
<style lang="">
    
</style>