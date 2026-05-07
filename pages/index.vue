<style>
.search-area:focus{
  border:0px solid #fff;
}

[contenteditable] {
  outline: 0px solid transparent;
}

.search-panel{
  margin:0 auto;width:550px;height:40px;padding:0.3em;border-radius:20px;text-align:center;border:1px solid #888;
}

.search-area{
  width:93%;float:left;height:35px;overflow:hidden;
}

.pagination {
    list-style: none;
    display: inline-block;
    margin:4px;
    cursor:pointer;
    border:1px solid gray;
    padding:0.4em;
}

.pagination:hover{
  background-color:#ddd;
}

.active{
  background-color:#0572d5;
  color:white;
}
</style>

<template>
<div class="container m-auto" style="margin-top:5px;margin-bottom:5px;background-color:white;padding:1em;">
<form method="post" action="">
  <div class="search-panel">
    <div id="search-area" class="search-area" contentEditable="true"></div>
    <div style="width:5%;float:left;"><button type="submit" style="border:0;padding:0;background-color:transparent;"><font-awesome icon="search" style="font-size:20pt;float:right;margin-right:10px;cursor:pointer;" title="search" /></button></div>
  </div>
  <input type="hidden" id="search-text" name="search-text"  placeholder="Search Here">
</form>
</div>

<div class="container m-auto" style="margin-top:5px;margin-bottom:5px;padding:5px;min-height:600px;box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;background-color:white;padding:20px;border-radius:5px;">
    <NuxtLink to="/book/create" class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2"><font-awesome icon="plus-circle" style="font-size:12pt;cursor:pointer;" />&nbsp;เพิ่มเอกสารใหม่</NuxtLink>
    <br><br>
    <table class="tbl" style="width:100%;">
    <tbody>
    <tr> 
        <th></th>
        <th>รหัสคีย์วิชา</th>
        <th>รหัสวิชา</th>
        <th>ชื่อวิชา</th>
        <th>ตอน</th>
        <th>ผู้สอน</th>
        <th>วัน</th>
        <th>เวลา</th>
        <th>ห้อง</th>
        <th></th>
      </tr>
      <tr v-for="(book,index) in state.books" :key="book.id">
                    <td style="width:5%;">{{book.id}}</td>
                    <td style="width:4%;padding:0.2em;">{{book.ae_code}}</td>
                    <td style="width:5%;">{{book.code}}</td>
                    <td style="width:20%;">{{book.subject}}</td>
                    <td style="width:10%;">{{book.sec}}</td>
                    <td style="width:5%;">{{book.teacher}}</td>
                    <td style="width:10%;">{{book.dates}}</td>
                    <td style="width:10%;">{{book.times}}</td>
                    <td style="width:10%;">{{book.room}}</td>
                    <td style="width:1%;">
                    <NuxtLink :to="`/book/${book.id}`" class="text-white bg-gradient-to-r from-blue-500 via-blue-600 to-blue-700 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-1 mb-1"><font-awesome icon="pencil" style="font-size:12pt;cursor:pointer;" /></NuxtLink>
                    </td>
        </tr>
        </tbody>
    </table>



</div>
</template>
<script setup lang="ts">

import axios from 'axios';
import { useGlobal } from '~/helpers/custom.js';
const p = useGlobal();

const state = reactive({
  url_endpoint:[],
  tokens:[],
  books:[],
  pages:[],
  rcordcnt:[],
  no:[],
  pagestext:[]
});

onMounted(() => {
    all();
    state.pages = 1;
});


async function all(){
 

            const config = {
                headers: {
                "Content-Type": "multipart/form-data",
                },
            };

              axios.get("http://localhost:5000/all")
                .then(response => {	
                state.books = response.data.data;  
                console.log(response.data.data);      
              }).catch(error => {
                alert(error);
              });

         
}



     
</script>