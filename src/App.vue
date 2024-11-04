<!-- โครงสร้าง #ประกอบด้วย 3 ส่วน-->

<!-- Javascrict #สำหรับเขียนคำสั่ง -->
<script>
export default {
  name:'App',
  data(){    // ** การกำหนดค่าหรือข้อมูลภายใน component ต้องกำหนดผ่าน function data() **
    return{ 
      firstName:"Supakun",
      lastname:"Thata",
      age:15,
      address:"<i>Chaing Rai</i>",
      picture:"https://w7.pngwing.com/pngs/340/946/png-transparent-avatar-user-computer-icons-software-developer-avatar-child-face-heroes-thumbnail.png",
      size:150,
      social:"https://www.facebook.com/",
      hobby:["เล่นเกมส์","ฟังเพลง","ดูหนัง"], //** เก็บข้อมูลเป็น Arrays
      general:{gender:'male', weight:65.5, height:170, status:false} //** เก็บข้อมูลเป็น Object
    }
  },
    methods:{ // ** การสร้าง function ต้องสร้าง ภายใน methods **
      getFullName(){
        return this.firstName + " " + this.lastname // ** เมื่อจะอ้างอิง Props ภายใน script ห้องใส่ this แต่ใน template จะใช้ {{}}**
      },
      showData(){
        alert(this.firstName)
      },
      increment(value){ // func เพิ่มอายุ
        return this.age += value
      },
      decrement(value){ // func ลดอายุ
        return this.age -= value
      }
    }
}
</script>

<!-- Component #สำหรับแสดงผล -->
<template>
  <section>
    <img v-bind:src="picture" :height="size"/> <!-- v-bind #เป็นการผูกข้อมูลนั้นกับ tag ที่เราสนใจ **  -->
    <h1>Name : {{ firstName }}</h1>
    <h1>Lastname : {{ lastname }}</h1>
    <h1>Age : {{ age }}</h1>
    <h1>Address : <span v-html="address"/></h1> <!-- v-html #เป็นการนำเอาString ที่มี tag html ออกมาโดยไม่มี tag นั้นแสดง **  -->
    <h1>Fullname : {{ getFullName() }}</h1>
    <h1>Social : <a :href="social" target="_blank">Facebook</a></h1>
    <h1>Hobby : 
      <ul>
        <li>{{ hobby[0] }}</li>
        <li>{{ hobby[1] }}</li>
        <li>{{ hobby[2] }}</li>
      </ul>
    </h1>
    <h1>General : 
      <ul>
        <li>gender : {{ general.gender }}</li>
        <li>weight : {{ general.weight }} kg</li>
        <li>height : {{ general.height }} cm</li>
        <li>status : {{ general.status }}</li>
      </ul>
    </h1>
    
    <!-- Add Event -->
    <h1>
      <button v-on:click="showData">คลิกเพื่อดูข้อมูล</button> <!-- v-on #เป็นการเรียกใช้ event ที่สนใจ **  -->
      <!-- <button @click="showData">คลิกเพื่อดูข้อมูล</button> @click #ลดรูป v-on:click **  -->
    </h1>
    <div class="box-btn">
      <button @click="increment(10)">เพิ่ม +</button>
      <button @click="decrement(5)">ลด -</button>
    </div>
  </section>
</template>

<!-- CSS Style -->
<style scoped>
.box-btn{
  display: flex;
  gap: 10px;
  margin-top: 10px;
}
</style>

