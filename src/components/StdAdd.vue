<script setup>
import img1 from '../assets/m1.jpg'
import img2 from '../assets/m2.jpg'
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
    <img :src="img1" alt="" width="150px " class="pic1"
    />
    <img :src="img2" alt="" width="150px" class="pic2" 
    />
  </div>
  <div class="StdAdd">
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
  <div >
  <button class="ButtonEdit" @click="showedit">แก้ไขข้อมูล</button>
  <br>
  <button class="ButtonSubmit" @click="SubmitEdit(Edit)" v-if="ShowEdit">ยืนยันแก้ไขข้อมูล</button>
  <button class="ButtonCancel" @click="reset" v-if="ShowEdit">ยกเลิก</button>
  </div>
</template>


<style>
  .pic1{
    margin-left: 10px ;
    margin-bottom: 30px ;
    border: 5px solid pink;
    border-radius: 10px ;
  }
  .pic2{
    margin-left: 100px ;
    border: 5px solid pink;
    border-radius: 10px ;
  }
  .StdAdd{
    padding: 40px;
    color: aquamarine;
    width: 700px;
    height: 250px;
    border: 2px solid red;
    background-color: black ;
    border-radius: 10px ;
  }
  .ButtonEdit{
    width: 100px ;
    height: 40px ;
    margin-top: 10px ;
    color: black;
    border-radius: 10px;
    background-color: yellow ;
    margin-bottom: 10px ;
  }
  .ButtonSubmit{
    width: 130px;
    background-color: rgb(0, 255, 0);
    margin-right: 10px ;
    border-radius: 10px ;
  }
  .ButtonCancel{
    width: 60px ;
    background-color: red ;
    border-radius: 10px ;
  } 
</style>