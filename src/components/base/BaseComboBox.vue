<template>
    <div class="drop-down">
            <div class="drop-down-box" data-id = "1">
                <input type="text" class="combo-box-input" id="textPosition-form" v-bind:filter="type" v-if="mode==1">
                <div class="drop-down-icon" id="position-form-icon" v-on:click="showDataCombobox">
                    <i class="fas fa-chevron-down "></i>
                </div>
            </div>
            <ul class="drop-down-list Position-form" v-bind:class="{ 'combobox-data-active': isActive}">
                <li class="drop-down-item" v-for="item in items" :key="item[typeName]" >
                    <!-- <div class="tick-item">

                    </div> -->
                    <span> {{item[typeName] }}</span>
                </li>
            </ul>
        </div>                                 
</template>
<script>
import axios from 'axios';
export default {
    name: 'Combobox',
    props:["type", "api", "data", "mode"],
    data(){
        return{
            isActive:false,
            value:"",
            current: 0,
            isDataLoaded: false,
            typeName: this.type + "Name",
            items: this.data,
            map: {
                Position: " Vị trí",
                Department: " Phòng ban",
            }
            
        }
    },
    created(){
        axios.get(this.api).then(res=>{
            console.log(res);
            this.items = [];
            if(this.mode == 1){
                this.items.push({
                    [this.typeName]:"Tất cả" + this.map[this.type]
                })
            }
            res.data.forEach(element => {
                this.items.push(element);
            });
        }).catch(err => {
            console.log(err);
        })
    },
    methods: {
        showDataCombobox(){
            this.isActive = !this.isActive;
            console.log("click");
        }
    }
}
</script>
<style scoped>
    @import '../../css/common/dropdown.css'
</style>