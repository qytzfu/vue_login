<template>
  <div class="container">
      <form action="" role="form">
          <div class="form-group">
              <label for="username">用户名:</label>
              <input type="text" id="username" class="form-control" placeholder="输入用户名" v-model="username">
          </div>
          <div class="form-group">
              <label for="age">年龄:</label>
              <input type="text" id="age" class="form-control" placeholder="输入年龄" v-model="age">
          </div>
          <div class="form-group">
              <input type="button" value="添加" class="btn btn-primary" v-on:click="add()">
              <input type="reset" value="重置" class="btn btn-danger">
          </div>
      </form>
      <hr>
      <table class="table table-hover">
        <caption class="h2 text-info text-center">用户信息表</caption>
        <thead>
          <tr class="text-danger">
            <th class="text-center">序号</th>
            <th class="text-center">名字</th>
            <th class="text-center">年龄</th>
            <th class="text-center">操作</th>
          </tr>
        </thead>
        <tbody>
          <!-- v-bind:key 这里绑定name不好,并不唯一,暂时先这样,后可以绑定index? -->
          <tr class="text-center" v-for="(item,index) in profile" v-bind:key="index">
            <td>{{index+1}}</td>
            <td>{{item.name}}</td>
            <td>{{item.age}}</td>
            <td>
                  <button class="btn btn-primary btn-sm" data-toggle="modal" data-target="#layer" v-on:click="nowIndex=index">删除</button>
            </td>
          </tr>
          <tr v-show="profile.length!=0">
              <td colspan="4" class="text-right">
                  <button class="btn btn-danger btn-sm" data-toggle="modal" data-target="#layer" v-on:click="nowIndex=-5">删除全部</button>
              </td>
          </tr>
          <tr v-show="profile.length==0">
              <td colspan="4" class="text-center text-muted">
                  <p>暂无数据....</p>
              </td>
          </tr>
        </tbody>
      </table>
      <!-- 弹出框 -->
      <div role="dialog" class="modal fade" id="layer">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <button type="button" class="close" data-dismiss="modal">
                <span>&times;</span>
              </button>
              <h4 class="modal-title">确定要删除么</h4>
            </div>
            <div class="modal-body">
              <button data-dismiss="modal" class="btn btn-primary btn-sm">否</button>
              <button data-dismiss="modal" class="btn btn-danger btn-sm"  v-on:click="deleteLine(nowIndex)">是</button>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>




<script>
export default {
  name: 'hello',
  data () {
    return {
      profile:[],
      username:'',
      age:'',
      nowIndex:-10,
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    add:function(){
      this.profile.push({
        name:this.username,
        age:this.age
      });
      console.log(this.username);
      console.log(this.age);
      this.username='';
      this.age='';
      // alert(this.profile)
      console.log(this.profile);
    },
    deleteLine:function(n){
      // 删除全部设置的值
      if(n==-5){
        this.profile=[];
      }else{
        this.profile.splice(n,1);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
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
