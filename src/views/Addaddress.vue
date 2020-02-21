<template>
<div class="skin">
	<div class="content">
		<h1>{{result}}</h1>

			<p>addressId</p><input type="text" v-model="addressId">
			<p>userName</p><input type="text" v-model="userName">
			<p>streetName</p><input type="text" v-model="streetName">
      <p>postCode</p><input type="text" v-model="postCode">
			<p>tel</p><input type="text" v-model="tel">
			
			<p class="submit" @click="Addaddress()">提交</p>
  </div>
</div>
  

</template>

<script>
  import {currency} from './../util/currency'
  import axios from 'axios'
export default {
  data(){
    return{
      addressId:'',
      userName:'',
      streetName:'',
      postCode:'',
      tel:'',
      default:false,
      result:'Add address',
    }
  },
  methods:{
		ischeck(){
			this.default = !(this.default)
			console.log(this.default)
		},

    Addaddress(){
				axios.post("/users/addaddress",{
					  "addressId": this.addressId,
            "userName": this.userName,
            "streetName": this.streetName,
            "postCode": this.postCode,
            "tel": this.tel,
            "isDefault": this.default
				}).then((response)=>{
						var res = response.data
						if(res.status == '1'){
							this.result = res.result
						}else{
							this.result = res.result
							this.$router.push({path:'/address'})
						}
				})
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
  width: 40px;
	text-align: center;
	border: 2px solid #f77;
	height: 60px;
	letter-spacing: 1em;
	line-height: 40px;
	font-size: 40px;
}
</style>