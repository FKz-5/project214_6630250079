<script setup>
import StdAdd from './components/StdAdd.vue' 
import StdCourse from './components/StdCourse.vue'
</script>

<template>
    <div>
        <h1  class="nisitdata mx-2">ข้อมูลนิสิต</h1>
        <StdAdd />
        <h1 class="detail mx-1">รายละเอียดการเรียน</h1>
        <StdCourse />
    </div>
</template>

<style>
    .nisitdata{
        margin-top: 10px;
        height: 60px;
        width: 175px;
        color: black;
        background-color: rgb(204, 153, 255);
        border: 2px solid black ;
        border-radius: 10px;
    }   
    .detail{
        padding: 3px;
        margin-top: 20px ;
        color:black;
        height: 60px;
        width: 350px;
        background-color: rgb(204, 153, 255) ;
        border: 2px solid black;
        border-radius: 10px;
    }
</style>