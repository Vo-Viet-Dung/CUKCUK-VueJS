<template>
    <div>
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
</template>
<script>
export default {
    name: 'Combobox',
    props:["type", "api", "data", "mode"],
    data(){
        return{
            isActive:false,
            value:"",
            
        }
    }
}
</script>
<style lang="">
    
</style>