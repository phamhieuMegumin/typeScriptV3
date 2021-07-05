<template>
    <div>
        <ul class="list-jobs">
             {{ testRenser() }}
            <li class="job-items" v-for="(job, index) in getListOrder" :key="index">
                <div class="title">{{ job.title }}</div>
                <div class="locations">{{ job.locale }}</div>
                <div class="salary">{{ job.salary }}</div>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
import Job from '@/interfaces/Job'
import OrderTemp from '@/interfaces/OrderTemp'
import { computed, defineComponent, onMounted, PropType, watch, watchEffect } from 'vue'

export default defineComponent({
   props : {
       jobs :{
           required : true,
           type : Array as PropType<Job[]>
       },
       orderBy :{
           required : true,
           type : String as PropType<OrderTemp>
       }
   },
   beforeCreate(){
       console.log("before Create")
   },
    setup(props){
        const getListOrder = computed(()=>{
            return [...props.jobs].sort((a : Job, b: Job)=>{
                return a[props.orderBy] > b[props.orderBy] ? 1 : -1;
            })
        })
        // watch sự thay đổi của props
        // nếu watch sự thay đổi của 1 ref thì tham số thứ nhất là ref muốn watch
        watch(()=> props.orderBy ,()=>{
            console.log(props.orderBy)
        })
        // watchEffect luôn chạy ngay khi componet được khởi tạo
        // watch Effect tự động theo dõi các biến được sử dụng bên trong nó
        watchEffect(()=>{
            console.log(props.orderBy)
        })
        const testRenser = ()=>{
           console.log("render")
        }
        return {getListOrder, testRenser}
    },
    
    mounted(){
        console.log("Mouted")
    }
})
</script>

<style scoped>

</style>