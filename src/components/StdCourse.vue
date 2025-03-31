<script setup>
import axios  from 'axios';
import { ref,onMounted } from 'vue';
const api_endpoint = "http://localhost:3000/courses";
const data = ref({});
const ShowEdit = ref(false)
const ShowAddData = ref(false)


const Edit = ref({
    "id": "",
    "name": "",
    "credit": "",
    "grade": "",
})
const showedit = (info) =>{
    ShowEdit.value = true
    Edit.value = {...info};
}
const AddData = (info) =>{
    ShowAddData.value = true
    Edit.value = {...info};
}

const reset = () => {
  ShowEdit.value = false;
  ShowAddData.value = false;
  Edit.value = {
    id: "",
    name: "",
    credit: "",
    grade: "",
  };
}
onMounted (async()=>{
  const response = await axios.get(api_endpoint);
  data.value = response.data;
}
)
const SubmitEdit = async(data) => {
  const response = await axios.put(`${api_endpoint}/${data.id}`,data);
  location.reload(true);
}
const SubmitAdd = async(data) => {
  const response = await axios.post(api_endpoint,data);
  location.reload(true);
}
const Delete = async(id) =>{
  const response = await axios.delete(`${api_endpoint}/${id}`)
  location.reload(true);
}
</script>

<template>
    <div v-for="task in data" :key="task.id">
        รหัสวิชา : {{ task.id }}
        ชื่อวิชา : {{ task.name }}
        หน่วยกิต : {{ task.credit }}
        เกรด : {{ task.grade }}
        <button @click="showedit(task)">แก้ไขข้อมูล</button>
        <button @click="Delete(task.id)">ลบข้อมูล</button>
    </div>
    <div>
      <h4><button @click="AddData">เพิ่มข้อมูล</button></h4>
    </div>
    <div v-if="ShowAddData">
      <h1>เพิ่มข้อมูล</h1>
      รหัสวิชา : <input type="text" v-model="Edit.id"/>
      <br>
      ชื่อวิชา : <input type="text" v-model="Edit.name"/>
      <br>
      หน่วยกิต : <input type="text" v-model="Edit.credit"/>
      <br>
      เกรด : <input type="text" v-model="Edit.grade"/>
      <br>
      <button @click="SubmitAdd(Edit)">ยืนยันแก้ไขข้อมูล</button>
      <button @click="reset">ยกเลิก</button>
    </div>
    <div v-if="ShowEdit">
      <h1>แก้ไขข้อมูล</h1>
      รหัสวิชา : <input type="text" v-model="Edit.id" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ Edit.id }}</span>
      <br>
      ชื่อวิชา : <input type="text" v-model="Edit.name" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ Edit.name }}</span>
      <br>
      หน่วยกิต : <input type="text" v-model="Edit.credit" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ Edit.credit }}</span>
      <br>
      เกรด : <input type="text" v-model="Edit.grade" v-if="ShowEdit" />
      <span v-if="!ShowEdit">{{ Edit.grade }}</span>
      <br>
      <button @click="SubmitEdit(Edit)" v-if="ShowEdit">ยืนยันแก้ไขข้อมูล</button>
      <button @click="reset" v-if="ShowEdit">ยกเลิก</button>
    </div>

</template>

<style>
</style>