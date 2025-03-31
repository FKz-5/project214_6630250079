<script setup>
import karina from '../assets/apk.jpg'
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
    ShowAddData.value = false 
    Edit.value = {...info};
}
const AddData = (info) =>{
    ShowAddData.value = true
    ShowEdit.value = false
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
    <div class="StdCourse" v-for="task in data" :key="task.id">
        รหัสวิชา : {{ task.id }}
        ชื่อวิชา : {{ task.name }}
        หน่วยกิต : {{ task.credit }}
        เกรด : {{ task.grade }}
        <br>
        <div>
        <button class="ShowEdit" @click="showedit(task)">แก้ไขข้อมูล</button>
        <button class="Delete" @click="Delete(task.id)">ลบข้อมูล</button>
        </div>
    </div>
    <div >
      <h4><button class="AddButton" @click="AddData">เพิ่มข้อมูล</button></h4>
    </div>
    <div class="ShowAdd" v-if="ShowAddData">
      <h1>เพิ่มข้อมูล</h1>
      รหัสวิชา : <input type="text" v-model="Edit.id"/>
      <br>
      ชื่อวิชา : <input type="text" v-model="Edit.name"/>
      <br>
      หน่วยกิต : <input type="text" v-model="Edit.credit"/>
      <br>
      เกรด : <input type="text" v-model="Edit.grade"/>
      <br>
      <div>
      <button class="ButtonSubmit" @click="SubmitAdd(Edit)">ยืนยันแก้ไขข้อมูล</button>
      <button class="ButtonCancel" @click="reset">ยกเลิก</button>
      </div>
    </div>
    <div class="StdEdit" v-if="ShowEdit">
      <h1 class="Editdata">แก้ไขข้อมูล</h1>
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
      <div>
      <button class="ButtonSubmit" @click="SubmitEdit(Edit)" v-if="ShowEdit">ยืนยันแก้ไขข้อมูล</button>
      <button class="ButtonCancel" @click="reset" v-if="ShowEdit">ยกเลิก</button>
      </div>
    </div>
    <div class="pic3">
      <img :src="karina" alt="" width="150px" class="pic2" >
    </div>

</template>

<style>
  .ShowAdd{
    color: rgb(153, 204, 255);
  }
  .StdCourse{
    padding: 10px;
    margin-top: 5px ;
    width: 650px ;
    border: 2px solid black ;
    border-radius: 10px ;
  }
  .ShowEdit{
    width: 100px ;
    background-color: yellow ;
    border-radius: 10px ;
    margin-right:10px ;
  }
  .Delete{
    width: 80px ;
    background-color: red ;
    border-radius: 10px ;
  }
  .AddButton{
    padding: 10px ;
    width: 140px;
    height: 50px;
    background-color:rgb(153, 153, 255);
    border-radius: 10px ;
    margin-top: 10px ;
  }
  .EditButton{
    margin-bottom: 20px ;
  }
  .pic3{
    margin-top: 20px ;
  }
  .ButtonSubmit{
    width: 130px;
    background-color: rgb(0, 255, 0);
    margin-right: 10px ;
    margin-top: 10px ;
    border-radius: 10px ;
  }
  .ButtonCancel{
    width: 60px ;
    background-color: red ;
    border-radius: 10px ;
  } 
  .StdEdit{
    color: rgb(255, 255, 153) ;
  }
</style>;