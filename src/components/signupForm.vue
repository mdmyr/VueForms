<template>
  <form @submit.prevent="submitHandler">
      <label>Email:</label>
      <input type="text" required v-model="email">
     <label>Password:</label>
     <input type="password" required v-model="password">
     <div v-if="passwordError" class="error">{{passwordError}}</div>
  
    <label>Role:</label>
    <select v-model="roles">
        <option value="developer">WebDeveloper</option>
        <option value="Admin">Admin</option>
    </select>
   

 <label>Skills: </label>
 <input type="text" v-model="tempSkill" @keyup.ctrl="addSkill">
 <div v-for="skill in skills" :key="skill" class="pill">
      
      <span @click="deleteSkill(skill)">{{skill}}</span>
 </div>



    <div class="terms">
        <input type="checkbox" v-model="terms">
        <label>Accept terms and conditions.</label>
    </div>


   <div class="submit">
       <button>Create Account</button>
   </div>

</form>

<hr v-if="debug">
<p v-if="debug">
    email: {{email}}
    password:{{password}}
    roles:{{roles}},
    terms:{{terms}},
    tempSkill:{{tempSkill}},
    skills:{{skills}}
</p>

</template>

<script>
export default {
    props:[],

    data(){
        return{
            email:'  ',
            password:'',
            roles:' ',
            terms:false,
            tempSkill:null,
            skills:[],
            passwordError:'',

            debug:true
        }

    },

    methods:{
        addSkill(keypressed){
            console.log(keypressed)
            console.log("===>"+ this.skills.includes(this.tempSkill) + " and tempskill ==>" + this.tempSkill)
            if(!this.skills.includes(this.tempSkill)){
                     if(keypressed.key === ',' && this.tempSkill  )
                        {
                            console.log(keypressed.key)
                            this.skills.push(this.tempSkill)
                            this.tempSkill=''
                        }
            }
            else{
                this.tempSkill=''
            }
            
        },
        deleteSkill(skill){
            console.log("delete skill"+ skill )
            this.skills=this.skills.filter((item)=>{
                console.log(item)
                if(item === skill){
                    console.log("delete this " +item)
                    return false
                }
                else{
                    return true
                }
            })


        },
        submitHandler(){
    
     //validation
    this.passwordError = this.password.length >5 ? '':'Password must be atleast 6 chars long'
    console.log(this.passwordError);
    if(!this.passwordError){
        console.log("form details " + this.email + " " + this.password + " " + this.skills+ " " + this.terms)
    }

    //
     console.log(this.passwordError)
     
 },
    }
,

 
    //lifeCycle hooks
    mounted(){
        console.log("mounted:signupForm")
    },
    updated(){
        console.log("udpated:signupForm")
    },
    unmounted(){
        console.log("unmounted")
    }

    //endof LifeCycle hooks

}
</script>

<style>

form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 20px;
}

label{
    color:#aaa;
    display: inline-block;
    margin:25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select{
 display: block;
 padding: 10px 6px;
 width: 100%;
 box-sizing: border-box;
 border: none;
 border-bottom: 1px solid #ddd;
 color:#555;
}
input[type="checkbox"]{
    display: inline-block;
    width:16px;
    margin: 0 10px 0  0 ;
    position: relative;
    top:2px
}

.pill{
display: inline-block;
margin: 20px 10px 0 0 ;
padding: 6px 12px;
background:#eee;
border-radius: 20px;
font-size: 12px;
letter-spacing: 1px;
font-weight: bold;
color:#777;
cursor:pointer;
}

button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}

.error{
     text-align: left;
     color:red;
     font-size: 12px;
}


</style>