<script setup>
import img1 from '../assets/ap.jpg'
import img2 from '../assets/apk.jpg'
import axios  from 'axios';
import { ref,onMounted } from 'vue';
const api_endpoint = "http://localhost:3000/students";
const data = ref({});
const ShowEdit = ref(false)
const Edit = ref({
    "first_name": "",
    "last_name": "",
    "id": "",
    "major": "",
    "school": ""
})
const showedit = () =>{
    ShowEdit.value = true
    Edit.value = {...data.value};
}

const reset = () => {
  ShowEdit.value = false;
  Edit.value = {
    first_name: "",
    last_name: "",
    id: "",
    major: "",
    school: ""
  };
}
onMounted (async()=>{
  const response = await axios.get(api_endpoint);
  data.value = response.data;
}
)
const SubmitEdit = async(data) => {
  const response = await axios.put(api_endpoint,data);
  location.reload(true);
}

</script>

<template>
  <div>
    <img :src="img1" alt="" width="150px " class="mx-2 my-2"
    />
    <img :src="img2" alt="" width="150px" class=" mx-5 my-4" 
    />
  </div>
  <div>
    <h4>ชื่อ : <input type="text" v-model="Edit.first_name" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ data.first_name }}</span></h4>
    <h4>นามสกุล : <input type="text" v-model="Edit.last_name" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ data.last_name }}</span></h4>
    <h4>รหัสนิสิต : <input type="text" v-model="Edit.id" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ data.id }}</span></h4>
    <h4>สาขา : <input type="text" v-model="Edit.major" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ data.major }}</span></h4>
    <h4>โรงเรียนเดิม : <input class="school" type="text" v-model="Edit.school" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ data.school }}</span></h4>
  </div>
  <button @click="showedit">แก้ไขข้อมูล</button>
  <button @click="SubmitEdit(Edit)" v-if="ShowEdit">ยืนยันแก้ไขข้อมูล</button>
  <button @click="reset" v-if="ShowEdit">ยกเลิก</button>
</template>


<style>
  .school{
    width: 400px;
  }
</style>