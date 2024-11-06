<!-- โครงสร้าง #ประกอบด้วย 3 ส่วน-->

<!-- Javascrict #สำหรับเขียนคำสั่ง -->
<script>
export default {
  name: "App",
  data() {
    // ** การกำหนดค่าหรือข้อมูลภายใน component ต้องกำหนดผ่าน function data() **
    return {
      firstName: "Supakun",
      lastname: "Thata",
      age: 15,
      address: "<i>Chaing Rai</i>",
      picture:
        "https://w7.pngwing.com/pngs/340/946/png-transparent-avatar-user-computer-icons-software-developer-avatar-child-face-heroes-thumbnail.png",
      size: 150,
      social: "https://www.facebook.com/",
      hobby: ["เล่นเกมส์", "ฟังเพลง", "ดูหนัง"], //** เก็บข้อมูลเป็น Arrays
      general: { gender: "male", weight: 65.5, height: 170, status: false }, //** เก็บข้อมูลเป็น Object
      nickName: "",
      isVisible: false,
      salary: 20000,
    };
  },
  methods: {
    // ** การสร้าง function ต้องสร้าง ภายใน methods **
    // getFullName() {
    //   return this.firstName + " " + this.lastname; // ** เมื่อจะอ้างอิง Props ภายใน script ห้องใส่ this แต่ใน template จะใช้ {{}}**
    // },
    showData() {
      alert(this.firstName);
    },
    increment(value) {
      // func เพิ่มอายุ
      return (this.age += value);
    },
    decrement(value) {
      // func ลดอายุ
      return (this.age -= value);
    },
    // setNickName(event){
    //   console.log(event.target.value)
    //   this.nickName = event.target.value
    // },
    submitForm() {
      // event.preventDefault(); ไม่จำเป็นต้องใส่มี การ modefier event ไม่ให้ form refresh
      alert("Save data successfuly!!");
      this.nickName = this.$refs.nickNameEl.value; // แสดง tag ที่อ้างอิง
    },
    toggleVisible() {
      return (this.isVisible = !this.isVisible);
    },
    getRandomByMethods() {
      return Math.floor(Math.random() * 100);
    },
    addSalary(value) {
      this.salary += value;
    },
  },
  computed: {
    // จะเป็นพื้นที่สำหรับการเขียน logic ที่ต้องการใช้ค่าจาก data ในพื้นที่ของ template #บน template จะไม่นิยมเขียน logic
    // **จะมีการใช้งานต่อเมื่อค่าที่สนใจมีการเปลี่ยนแปลงเท่านั้นถ้าค่าไม่มีการเปลี่ยนแปลงแล้วถูกเรียกใช้งานจะแสดงผลลัพธ์ของค่าเดิมออกมาเพราะมีการแคชค่านั้นเก็บไว้
    getFullName() {
      return this.firstName + " " + this.lastname; // ** เมื่อจะอ้างอิง Props ภายใน script ห้องใส่ this แต่ใน template จะใช้ {{}}**
    },
    getRandomByComputed() {
      return Math.floor(Math.random() * 100);
    },
    getIncome() {
      return this.salary * 12;
    },
    getDepartment() {
      return this.salary >= 35000 ? "Project manager" : "Programmer";
    },
  },
};
</script>

<!-- Component #สำหรับแสดงผล -->
<template>
  <section>
    <!-- ref #เก็บการอ้างอิง tag นั้น -->
    <img v-bind:src="picture" :height="size" ref="imageURL" />
    <!-- v-bind #เป็นการผูกข้อมูลนั้นกับ tag ที่เราสนใจ **  -->
    <br />
    <h1>
      <form @submit.prevent="submitForm">
        <!-- @click.prevent (ไม่มีการ refersh) *** Event Modifier #เก็บการกำหนดเงื่อนไขต่างในการทำให้เกิด Event **  -->
        <label>Nickname : </label>
        <input type="text" v-on:input="setNickName" ref="nickNameEl" />
        <!-- v-on:input #เป็นการ get value จาก input เหมือน onChange แต่ใน vue จะเก็บค่าต้องใช้ v-on:input **  -->
        <button type="submit">Submit</button>
      </form>
    </h1>
    <h1>Name : {{ firstName }}</h1>
    <h1>Lastname : {{ lastname }}</h1>
    <h1>Nickname : {{ nickName }}</h1>
    <h1>Age : {{ age }}</h1>
    <h1>เงินเดือน : {{ salary }} บาท</h1>
    <h1>รายได้ต่อปี : {{ getIncome }} บาท</h1>
    <!-- computed ใช้กับ logic ที่มีการคำนวณ -->
    <h1>
      ตำแหน่งงาน : {{ getDepartment }}
      <!-- ตำแหน่งงาน : {{ salary >= 35000 ? "Project manager" : "Programmer" }} #จะไม่นิยมเขียน logic ** -->
    </h1>
    <button @click="addSalary(5000)" style="margin-right: 10px">
      เพิ่มเงินเดือน +
    </button>
    <button @click="toggleVisible">
      {{ isVisible ? "Hidden" : "Show" }} details
    </button>
    <article v-show="isVisible">
      <!-- isVisible เป็น true จะแสดง -->
      <h1>Address : <span v-html="address" /></h1>
      <!-- v-html #เป็นการนำเอาString ที่มี tag html ออกมาโดยไม่มี tag นั้นแสดง **  -->
      <h1>Fullname : {{ getFullName }}</h1>
      <!-- เป็น computed func สามาเรียกใช้แบบตัวแปลได้เลย ** ไม่ต้องมี ()  -->
      <h1>Social : <a :href="social" target="_blank">Facebook</a></h1>
      <div>
        <h1>
          Hobby :
          <!-- v-if, v-else -->
          <p v-if="hobby.length === 0">ไม่มีงานอดิเรก</p>
          <!-- v-if #กำหนดเงื่อนไขค่างๆ-->
          <ul v-else>
            <!-- v-else -->

            <!-- v-for #ใช้ดึงค่าจาก array or object **ต้องกำหนด key ด้วย-->
            <li v-for="(item, index) in hobby" :key="index">
              {{ index + 1 }}. {{ item }}
            </li>
            <!-- <li>{{ hobby[0] }}</li> -->
          </ul>
        </h1>
      </div>
      <h1>
        General :
        <ul>
          <!-- v-for #ใช้ดึงค่าจาก array or object **ต้องกำหนด key ด้วย-->
          <li v-for="(item, key) in general" :key="key">
            {{ key }} : {{ item }}
          </li>
          <!-- <li>gender : {{ general.gender }}</li> -->
        </ul>
      </h1>
    </article>

    <!-- Add Event -->
    <h1>
      <button v-on:click="showData">คลิกเพื่อดูข้อมูล</button>
      <!-- v-on:click #เป็นการเรียกใช้ event ที่สนใจ **  -->
      <!-- <button @click="showData">คลิกเพื่อดูข้อมูล</button> @click #ลดรูป v-on:click **  -->
    </h1>
    <div class="box-btn">
      <button @click="increment(10)">เพิ่ม +</button>
      <button @click.middle="decrement(5)">ลด -</button>
      <!-- @click.middle *** Event Modifier #เก็บการกำหนดเงื่อนไขต่างในการทำให้เกิด Event **  -->
    </div>
    <h1>ความแตกต่าง Medhods และ Computed</h1>
    <!-- ความแตกต่าง Medhods vs Computed -->

    <h2>- Methods1 : {{ getRandomByMethods() }}</h2>
    <h2>- Methods2 : {{ getRandomByMethods() }}</h2>
    <hr />
    <!-- Computed ค่าจะเป็นค่าเดิมเนื่องจากมีการแคชค่าที่สนใจไว้และค่าจะเปลี่ยนแปลงก็ต่อเมื่อค่าที่สนใจนั้นมีการเปลี่ยนแปลง -->
    <h2>- Computed1 : {{ getRandomByComputed }}</h2>
    <h2>- Computed2 : {{ getRandomByComputed }}</h2>
  </section>
</template>

<!-- CSS Style -->
<style scoped>
.box-btn {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}
</style>


<!-- Note -->
<!-- v-show vs v-if -->
<!--1. v-show #ซ่อนหรือแสดง elm นั้นออกมา โดยที่ elm นั้นมีอยู่แล้ว-->
<!--2. v-if #แทรก elm นั้นเลยโดยที่ elm นั้นไม่มีอยู่-->

