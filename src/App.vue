<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#">Disabled</a>
      </li>
    </ul>
    <div class="form-inline mr-3">
      <select name="" id="" class="form-control" @change="ChangeStatus" v-model="status">
        <option value="線上">線上</option>
        <option value="線下">線下</option>
      </select>
      Hi ,{{ShowUserName}}
    </div>
  </div>
</nav>
    <!-- <router-view :status="myStatus" @pushNewName="GetNewName"/> -->
    <router-view @pushNewName="GetNewName"/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      //  status:'線上',
      status:this.$store.state.status,
      // myStatus:'線上',
      username:'Andy'
    }
  },
  computed:{
    ShowUserName(){
      return this.$store.state.username
    }
  },
  methods:{
    ChangeStatus(){
      // this.myStatus = this.status;
      this.$store.state.status = this.status
    },
    GetNewName(newName){
      this.username=newName;
    }
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
