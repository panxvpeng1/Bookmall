<template>
<div class="skin">
	<div class="content">
		<h1>{{result}}</h1>
			<p>username</p><input type="text" v-model="username">
			<p>password</p><input type="text" v-model="password">
			<p>password</p><input type="text" v-model="password2">
			
			<p class="submit" @click="register1()">提交</p>
  </div>
</div>
  

</template>

<script>
  import {currency} from './../util/currency'
	import axios from 'axios'
	
export default {
  data(){
    return{
      username:'',
      password:'',
      password2:'',
      result:'',
    }
  },
  computed:{
    ComparePassword(){
			if(this.password2 != this.password2){
				this.result = '两次密码不一致'
			}
    },
  },
  methods:{
		
    register1(){
			if(this.userName == '' || this.password == '' ){
				this.result = '用户名或密码不能为空'
				return
			}else if(this.password != this.password2 ){
				this.result = '两次密码不一致哦'
				return
			}else{
				axios.post("/users/register",{
				userName:this.username,
        userPwd:this.password
			}).then((response)=>{
				var res = response.data	
				var x = res.result
				console.log(x)
				console.log(res.status)
				if(res.status == '1'){
					this.result =  x
				}
				if(res.status == '0'){
					console.log(res.status)
					this.result =  x
					this.$router.push({path:'/'})
				}
			});
			}
			
		}
		
  },

}
</script>

<style scoped>
.submit{
	cursor: pointer;
}
h1{
	color: red;
}
p{
	font-weight: bolder;
	font-size: 28px;
}
.skin{
	height: 100%;
	width: 100%;
	background-image: url(./../../static/fish.jpg);
	background-size:cover;
}
.content{
	margin:100px auto; 
	background: #aaa;
	width: 600px;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction:column;
}
input{
	flex: 1;
	width: 600px;

}
button{
	text-align: center;
	border: 2px solid #f77;
	height: 60px;
	letter-spacing: 1em;
	line-height: 40px;
	font-size: 40px;
}
</style>

