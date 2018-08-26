<template>
  <div class="hello container-fluid mt-5">
    <div>
      狀態：{{ShowStatus}}
    </div>
    <div class="form-inline">
      <input type="text" class="form-control mr-1" v-model="username">
      <button type="text" class="btn btn-primary mr-1" @click="UpdateUsername">更新姓名</button>
    </div>
    <table class="table">
    <thead>
      <tr>
        <th scope="col">序號</th>
        <th scope="col">圖片</th>
        <th scope="col">姓名</th>
        <th scope="col">EMail</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item,index) in ListData" :class="{'bg-info':item.selected}">
        <th scope="row">{{index + 1}}</th>
        <td><img :src="item.picture.medium"></td>
        <td>{{item.name.first + ' ' + item.name.last}}</td>
        <td>{{item.email}}</td>
        <td>
          <button class="btn btn-outline-primary" @click="ClickMe(item)">點我</button>
          </td>
      </tr>
    </tbody>
  </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  // props: ["status"],
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      ListData: [],
      username: "Andy",
      status:this.$store.state.status
    };
  },
  methods: {
    getData() {
      let vm = this;
      this.axios
        .get("https://randomuser.me/api/?results=50")
        .then(function(response) {
          vm.ListData = response.data.results;
          vm.ListData.forEach(function(item){
            vm.$set(item,'selected',false);
          });
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    UpdateUsername() {
      // let vm = this;
      // vm.$emit('pushNewName',vm.username)
      this.$store.state.username = this.username
    },
    ClickMe(item){
      item.selected = !item.selected
      console.log(item.selected)
    }
  },
  computed:{
    ShowStatus(){
      return this.$store.state.status
    }
  },
  mounted() {
    this.getData();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
