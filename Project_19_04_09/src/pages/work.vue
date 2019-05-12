<template>
  <div>

    <div class="input">
      <span> Name:</span> <input type="text" v-model="name"><br>
      <span> Age:</span> <input type="text" v-model="age"><br>
      <span> Sex:</span> <select name="sex" id="sex" v-model="sex">
        <option value="Male">male</option>
        <option value="Female">female</option>
      </select>
      <br>
      <button @click="creat">Create</button>
    </div>

    <div style="clear: both"></div>

    <div class="table" style="width:600px; margin-left:50px;">
      <table class="table table-bordered table-striped">
        <thead>
          <tr style="background: rgb(51, 221, 164)">
            <th>Name</th>
            <th><span @click="agePx()" id="agePx">Age</span></th>
            <th>Sex</th>
            <th>Delete</th>
          </tr>
        </thead>
        <tbody id="tbody">
          <tr v-for="(item, index) in items" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.age }}</td>
            <td>{{ item.sex }}</td>
            <td><button @click="delete1(index)" >Delete</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

</template>

<script>
  export default {
    data(){
      return {
        index: 0,
        name: '',
        age: '',
        sex: 'Male',
        items: [
          {
            name: 'Jack',
            age: 30,
            sex: 'Male'
          },
          {
            name: 'Bill',
            age: 26,
            sex: 'Male'
          },
          {
            name: 'Tracy',
            age: 22,
            sex: 'Female'
          },
        ]
      }
    },
    methods:{
      creat() {
        let item = {
          name: this.name,
          age: parseInt(this.age),
          sex: this.sex
        }
        this.items.push(item)
      },
      delete1(index){
        this.items.splice(index, 1)
      },
      agePx(){
        if (this.index ===0) {
          this.items.sort(compare('age'))
          this.index = 1;
        }
        else {
          this.items.sort(compare('age'))
          this.items.reverse()
          this.index = 0;
        }

        // var i = 0;
        // return function () {  
        //   if (i === 0) {
        //     this.items.sort(compare('age'))
        //     i = 1
        //   }
        //   else{
        //     this.items.sort(compare('age'))
        //     this.items.reverse()
        //     i = 0
        //   }
        // }
      }
    }
  }

// function getIndex (_arr,_obj) {
//   var len = _arr.length;
//   for(var i = 0; i < len; i++)
//   {
//     if(_arr[i] == _obj)
//     {
//         return parseInt(i);
//     }
//   }
//   return -1;
// };

function compare(property) {  
  return function(a, b) {
    var value1 = a[property]
    var value2 = b[property]
    return value1 - value2
  }
}

function a() {  
  var i = 1;
  console.log(i)
  return function () {  
    i += 1
    console.log(i)
  }
}
a()()
</script>

<style scoped>
  .input{
    border: 1px solid red;
    padding: 20px;
    float: left;
    margin-left: 20px;
    text-align: start;
    margin-bottom: 20px;
  }
  .input span{
    display: inline-block;
    width: 50px;
    margin: 10px 0;
    text-align: end;
  }
  thead th{
    text-align: center;
  }
  #agePx:hover{
    background-color: rgb(164, 226, 18);
  }
</style>


