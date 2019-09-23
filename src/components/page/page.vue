<template>
  <section>
    <div class="container">
      <div class="title">
        <input type="text" placeholder="name" v-model.trim="input.name">
        <input type="text" placeholder="phone" v-model.trim="input.phone">
        <input type="text" placeholder="email" v-model.trim="input.email">
        <button @click="submitHandler"> save</button>
        <button @click="cancelHandler">cancel</button>
      </div> 
      <div class="menu">
        <ul class="menuNav">
          <li>NO</li>
          <li>Name</li>
          <li>Phone</li>
          <li>email</li>
          <li>edit</li>
          <li>delete</li>
        </ul>
        <ul v-for="(item,index) in contact" class="meenuItem">
          <li>{{index+1}}</li>
          <li>{{item.currentName}}</li>
          <li>{{item.currentPhone}}</li>
          <li><a href="'mailto:'+item.currentEmail">{{item.currentEmail}}</a></li>
          <li @click="editHandler(index)"><img src="@/../src/assets/edit.svg" alt="edit"></li>
          <li @click="deleteHandler(index)"><img src="@/../src/assets/delete.svg" alt="delete"></li>
        </ul>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  data() {
    return{
      //讀取判斷
      // loading: false,
      editIndex: null,
      //資料
      input:{
        name:'',
        phone:'',
        email:''
      },
      contact:[
        {
          currentName:'sam',
          currentPhone:'phone',
          currentEmail:'email'
        }
      ]
    }
  },
  methods:{
    submitHandler(){
      // let{name, phone, email} = this.input
      // if(!name || !phone || !email) return
      this.Check()
      if(this.input.name && this.input.phone && this.input.email){
        if(this.editIndex==null){
          this.contact.push({
            currentName: this.input.name,
            currentPhone: this.input.phone,
            currentEmail: this.input.email
          })
          this.cancelHandler()
        }else{
          this.contact[this.editIndex].currentName = this.input.name
          this.contact[this.editIndex].currentPhone = this.input.phone
          this.contact[this.editIndex].currentEmail = this.input.email
          this.cancelHandler()
        }
      }
    },
    cancelHandler(){
      this.editIndex = null
      this.input={
        name:'',
        phone:'',
        email:''
      }
    },
    deleteHandler(index){
      let target = this.contact[index]
      if(confirm(`確定刪除 ${target.currentName} ?`)){
        this.contact.splice(index, 1)
      }
      this.cancelHandler()
    },
    editHandler(index){
      this.editIndex = index  
      this.input.name = this.contact[index].currentName
      this.input.phone = this.contact[index].currentPhone
      this.input.email = this.contact[index].currentEmail
    },
    Check(){
      // let name = this.input.name
      // let mail = this.input.email
      // let phone = this.input.phone
      let emailCheck = false
      let phoneCheck = false
      let emailRegex = /[\w\-\.]+@[\w\.]+/g;
      let phoneRegex = /^[\d\+\-]+[\d\+\-]+[\d\+\-]*$/;
      let arr = Object.keys(this.contact)
      let len = arr.length;
      for(var i=0 ; i<len ; i++){
        if(this.input.name != this.contact[i].currentName){
          // console.log(len ,  this.contact[i].currentName , this.input.name);
        }else{
          this.input.name=""
          console.log("name repeated : " + this.contact[i].currentName)
        }
      }
      if(phoneCheck = phoneRegex.test(this.input.phone) ){
        // console.log(phoneCheck)
      }else{
        this.input.phone=""
        console.log(" Digit and character + , - only.")
      }
      if( emailCheck = emailRegex.test(this.input.email) ){
        // console.log(emailCheck)
      }else{
        this.input.email=""
        console.log("email format")
      }
    }
  },

}
</script>


<style lang="scss" scoped>
@import './page.scss'
</style>
