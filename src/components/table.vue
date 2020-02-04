<template>


    <div >
        <div class="container">
            <div class="row">
                <div class="col-md-8">
                        <table class="table border">
                                <thead>
                                <tr>
                                    <th scope="col">id</th>
                                    <th scope="col">name</th>
                                    <th scope="col">role</th>
                                    <th scope="col">email</th>
                                    <th scope="col">sex</th>
                                
                                </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="(person,index) in persons" :key="index">
                                            <th scope="row">{{parseInt(index) +1}}</th>
                                            <td>{{person.name}}</td>
                                            <td>{{person.role}}</td>
                                            <td>{{person.email}}</td>
                                            <td>{{person.sex}}</td>

                                            <td>
                                                <button class="btn btn-danger" @click="removeItem(index)">X</button>
                                                <button class="btn btn-info ml-2" @click="updateItem(person)">E</button>
                                            </td>
                                    </tr>
                                    
                                    
                                </tbody>
                        </table>
                </div>

                <div class="col-md-4">
                    <div class="card shadow p-4">
                        <h2 class="mb-4">Please Add New Users</h2>
                        

                        <form @submit.prevent="addUser">
                                <div class="form-group">
                                    <label>Name</label>
                                    <input v-model="user.name" type="text" id="name" class="form-control">
                                </div>
                                <div class="form-group">
                                        <label>Role</label>
                                        <input v-model="user.role" type="text" id="role" class="form-control">
                                </div>
                                 <div class="form-group">
                                        <label>Email</label>
                                        <input v-model="user.email"  type="text" id="role" class="form-control">
                                </div>
                                 <div class="form-group">
                                        <label>Sex</label>
                                        <select class="form-control" v-model="user.sex">
                                            <option disable selected>Please Choose</option>
                                            <option value="male">Male</option>
                                            <option value="female">Female</option>
                                        </select>
                                </div>
                                <div class="form-group">
                                        
                                        <button v-if="status" @click="validEmail" type="submit" class="btn btn-primary" >submit</button>
                                        <button v-else type="click" @click.prevent="updatePerson()" class="btn btn-primary" >update</button>
                                        <button type="reset" id="reset" class="btn btn-danger" style="margin-left:20px;">reset</button>
                                        
                                </div>
                        </form>
                    </div>
                   
                </div>
            </div>
        </div>
    </div>

</template>

<style scoped>
.edit{
    background-color: hsl(2,4,7) !important;
}
</style>

<script>
import swal from 'sweetalert'
import Swal from 'sweetalert2'
export default {
    
    data(){
        return{
            user: {
            name: "",
            role: "",
            sex:'',
            email:''
            },

            status: true,

            persons: [
            {name:"Mercy", role:"Vuejs dev ", email:"udohmercy911@gmail.com",sex:'female'},
            {name:"Amaka", role:"JS dev", email:"ammy1130@gmail.com",sex:"female"},
            {name:"Dora", role:"UI/UX dev", email:"nyonganniebiet@gmail.com",sex:"female"},
            {name:"Ekemini", role:"CSS dev", email:"kemzytony@gmail.com",sex:"female"},
            {name:"Imeh", role:"Laravel dev", email:"mosco4peace@gmail.com",sex:"male"}
            ]
        }
    },
    
    methods: {

addUser() {
    
    swal({
  title: "Are you sure you want to add this user?",
  text: "",
  icon: "info",
  buttons: true,
  dangerMode: false,
})
.then(willAdd => {
  if (willAdd) {
      if(this.user.name === ''|| this.user.role==='' || this.user.email === '' || this.user.sex==='') {
          return swal('Error','Please fill the form correctly','error')
      }
      else if (!this.validEmail(this.user.email)) {
        return swal('Error','Email is not valid','error')
      }
      else {
      this.persons.push(this.user)
      }
    swal("This user has been added", {
      icon: "success",
    });
  } else {
    swal("Your imaginary file is safe!");
  }
});
},
        removeItem(index){
            // this.persons.splice(index,1);
                Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
        }).then(WillDelete => {
        if (WillDelete) {
         this.persons.splice(index,1);  
            Swal.fire(
            'Deleted!',
            'Your file has been deleted.',
            'success'
            )
  }
})
           
        },
        updateItem(id){
            // console.log(id);
            // this.user.name = id.name;
            // this.user.role = id.role;
            this.user = id;
            this.status = !this.status;
            
        },
        updatePerson(index){
            this.persons.push(index);
        },
        validEmail(email){
            let isValid = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email)
            return isValid
        }
        
    }

}
</script>