<template>
  <section>
   <img :src="picture" :width="size" :height="size" ref="imageEl">
    <form @submit.prevent="submitForm2"> prevent คือล็อกค่าหน้าจอไม่รีเฟรช <br>
        <label for="">ป้อนชื่อเล่น</label>
        <input type="text"  ref="nicknameEl">
        <button type="submit">บันทึก</button>
    </form>
          <h1>ชื่อพนักงาน: {{getfullname}} </h1>
          <h1>ชื่อเล่น: {{Nickname}}</h1>
          <h2>อายุ:{{Old}}</h2>
          <h2>เงินเดือน: {{salary}} บาท</h2>
          <h2>รายได้ต่อปี: {{getincome}} บาท</h2>
          <h1>ตำแหน่งงาน : {{getDepartment}}</h1>
          <button @click="getincrementsarary(5000)">เพิ่มเงินเดือน</button>
          <hr>
          <h2>Method1 : {{getRandomMethod()}}</h2>
          <h2>Method2 : {{getRandomMethod()}}</h2>
          <hr>
          <h2>Computed1 : {{getRandomCompute}}</h2>
          <h2>Computed2 : {{getRandomCompute}}</h2>
          {{isVisible}}
          <button @click="toggleVisible" >{{isVisible ? "ซ่อน" : "แสดง"}}รายละเอียด</button>
    <article v-show="isVisible">
        <p>ที่อยู่: <span v-html="address"></span></p>
        <p>Social <a :href="social" target="_blank">Facebook</a></p>
        <p v-if="hobby.length === 0 ">ไม่มีงานอดิเรก</p>
      <div v-else>
        <p>งานอดิเรก</p>   
        <ul>
          <li v-for="(item,index) in hobby" :key="index">{{index}}-{{item}}</li>
        </ul>
      </div>
        <p>ข้อมูลพื้นฐาน</p>
        <ul>
          <li v-for="(item,data) in general" :key="data">{{data}}-{{item}}</li>
        </ul>
      <button @click="showdata">ดูข้อมูล</button>
      <button @click.ctrl="increment(10)">เพิ่ม</button>
      <button @click.middle="decrement">ลด</button>
    </article>
  </section>
</template>
<script>
export default {
 name: 'App',
 data(){
   return{
       firstname: "Mark",
       lastname: "Prarod9",
       Nickname: "",
       Old: 18,
       address:"<i>Udonthani</i>",
       picture:"https://cdn-icons-png.flaticon.com/512/560/560277.png",
       size:150,
       social:"https://www.facebook.com/markvebber2/",
       hobby:["เล่นเกม","ทำสวน","ฟังเพลง","เล่นน้ำ","ตัดผม","นั่งเล่น"],
       general:{gender:"ชาย",weight:68 ,height:190,status:false},
       isVisible:false,
       salary:20000
   }
 },
 
 methods:{
   
   showdata(){
     alert(this.firstname)
   },
   increment(value){
     this.Old+=value
   },
   decrement(){
     this.Old--
   },
   setNickname(event){
     console.log(event.target.value),
     this.Nickname=event.target.value
     //event.target.value คือการโชว์ค่าตอนพิมพ์แบบrealtime
   },
   submitForm(){
    //e.preventDefault();
     console.log(this.$refs.imageEl);
     alert("บันทึกชื่อเล่นเรียบร้อย")
   },
   submitForm2(){
    //e.preventDefault();
     this.Nickname=this.$refs.nicknameEl.value;
   },
   toggleVisible(){
    //e.preventDefault();
     this.isVisible =!this.isVisible
   },
   getRandomMethod(){
    return Math.random();
   },
   getincrementsarary(value){
     this.salary += value;
   }
 },
 computed:{
  getfullname(){
     return this.firstname + " "+ this.lastname 
   },
   getRandomCompute(){
    return Math.random();
   },
   getincome(){
    return this.salary*12;
   },
   getDepartment(){
    return this.salary >= 35000 ? "ProjectMenager": "Programmer";
   },
   
 },
 watch:{
    salary(value){
        if(value>50000){
          alert("เงินเดือนไม่ควรเกิน 50000 บาท");
          setTimeout(() => {
            this.salary=50000
          }, 500);
        }
    }
 }
 
}
</script>
<style></style>
