<template>
  <h1>Hello</h1>
  <p>AtistName {{user}} with the picture title {{ employee }} </p>
  <button @click="changeName">Change name</button>
  <button @click="changeOrder('title')">Orderby Title</button>
  <button @click="changeOrder('locale')">Orderby Local</button>
  <button @click="changeOrder('salary')">Orderby Salary</button>
  <JobList :jobs="listJob" :orderBy="orderBy"/>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from 'vue';
import Job from "../src/interfaces/Job"
import JobList from "./components/JobList.vue"
import OrderTemp from "./interfaces/OrderTemp"
export default defineComponent({
  name: 'App',
  components : {
    JobList
  },
  data(){
    return{
       employee : "PQ nam"
    }
  },
 setup(){
  //  const state = reactive({
  //    user : "Leonado Davinci",
  //    title : "To day so cool" as string | number, // xet giá trị cho title là string hoặc number, với data() tương tự
  //    age : 30
  //  })
  //  state.title = "Monalisa"
  //  return toRefs(state)
  const user = ref("Leonado Davinci");
  const title = ref<string | number>("To day so cool");
  const listJob = ref<Job[]>([
    {title : "Nhan vien ban hang", locale : "Ha noi", salary : 23000},
    {title : "Giám đốc", locale : "Nam định", salary : 22000},
    {title : "Thử việc", locale : "Ý yên", salary : 32000},
    {title : "Kinh doanh", locale : "Cao bằng", salary : 12000},
  ])
  const orderBy = ref<OrderTemp>()
  const changeOrder = (a : OrderTemp)=>{
    orderBy.value = a
  }
  user.value = "To ngoc van"
  return {user, title, listJob, orderBy, changeOrder}
 },
 methods:{
   changeName(){
     this.user = "Change name to any"
   }
 }
});
</script>

<style>

</style>
