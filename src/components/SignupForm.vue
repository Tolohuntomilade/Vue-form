<template>
   <form @submit.prevent="handleSubmit">
       <!-- This submit modiffier prevent, it prevents the window from refreshing when the submit buttion is clicked -->
      <label>Email:</label>
      <input type="email" required v-model="email">
      <!-- v-model allows us to keep track of update made to the weither an input or select boxes and it allows two way data binding thatis input to component and also component to input -->
      <label>Password:</label>
      <input type="password" required v-model="password">
      <div v-if="passwordError" class="error">{{passwordError}}</div>
      <!-- This checks if passwordError function is true and then fires it defined role -->

      
      <label>Role:</label>
      <select v-model="role">
          <option value="developer">Web Developer</option>
          <option value="designer">Graphics Designer</option>
      </select>

      <label>Skills:</label>
      <input type="text" v-model="tempSkills" @keyup.ctrl="addSkills">
      <!--  Key event modiffer: This is  needed for .ctrl is to prevent adding comma . Hence after writing out the skill you click ctrl+,-->
      <div v-for="skill in skills" :key="skill" class="pills" >
          <!-- looping through the skills array and also data binding a unique key to this by using skill which is unique to the alone -->
          <span @click="removeSkills(skill)">
              <!-- This activate the removeSkills function that takes in skill been clicked on as a parameter -->
            {{skill}}  
          </span>
         
      </div>


      <!-- V-model for checkbox with compulsory single input -->
      <div class="terms">
          <input type="checkbox"  v-model="terms" required>
          <label>Accept all terms and conditions</label>
      </div>
  
      <!-- V-model for multiple checkbox -->
      <!-- <div>
          <input type="checkbox" value="maryam" v-model="names">
          <label>Maryam</label>
      </div>
       <div>
          <input type="checkbox" value="rilwan" v-model="names">
          <label>Rilwan</label>
      </div>
       <div>
          <input type="checkbox" value="fashola" v-model="names">
          <label>Fashola</label>
      </div> -->

      <div class="submit">
          <button>Create an Account</button>
      </div>
    </form>

    <!-- <p> Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>terms: {{terms}}</p>
    <p>skills: {{skills}}</p> -->
    <!-- <p>names: {{names}}</p> -->
</template>

<script>
export default {
    data() {
        return {
            // email:"mario",
            // This shows the effect of the componet to input data binding
            email:"",
            password:"",
            role:"",
            // role:"designer"
            // This shows the effect of the componet to input data binding, that is giving the select box a default value
            terms: false,
            //Terms is set to false if you want the checkbox unclicked by default or set to true if you want it clicked by default
            // names:[]
            tempSkills:"",
            skills:[],
            passwordError:''
           
        }
    },
    methods: {
        addSkills(e){
           if (e.key==="," && this.tempSkills) {
               if (!this.skills.includes(this.tempSkills)) {
                   this.skills.push(this.tempSkills)
                //    this mainly checks if a function is in the array and does add only an array onces in order to prevent redundancy
               }
               
               this.tempSkills=""
            //    after the if statement had been carried out it clears out the input box
           }
        },
        removeSkills(skill){
            this.skills= this.skills.filter((item) =>{
               return skill !== item
               //This function removes a skill when clicked on that is it takes the clicked on skill as a parameter and filters it out of th array
            })

        },
        handleSubmit(){
            console.log("Form Submitted")
            //Validate Password
            this.passwordError = this.password.length>5? '': "Password must be at least 6 chars long"
            // This is activated after the submit button is clicked that is validation in order to ensure that the length of the password is 5 and if not gives an error messsage
            // if (this.password.length<5) {
            //     this.passwordError = "Password must be at least 6 chars long"
            // }
            // else{
            //     this.passwordError=""
            // }
            if (!this.passwordError) {
                console.log('email: ', this.email )
                console.log('password: ', this.password )
                console.log('role: ', this.role )
                console.log('skills: ', this.skills )
                console.log('terms: ', this.terms )

            // This displays the values in the console
            }
        }
    },
}
</script>

<style scoped>
    form{
        max-width: 420px;
        margin: 30px auto;
        background: #fff;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555; 
    }
    input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top:2px
    }
    .pills{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color:#777;
        cursor: pointer;
    }
    button{
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: #fff;
        border-radius: 20px;
    }
    .submit{
        text-align: center;
    }
    .error{
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>