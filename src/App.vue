<template>
	<div id="app">
		
		<div style="position: absolute;top: 200px;">
			<input type="radio" name="choose" value="根据总数" @click="isTotal()"  checked=""/>按人数
			<input type="radio" name="choose" value="根据文本域" @click="isText()"/>自定义
			<br /><br /><br />
			<div v-if="isChoose">
				<div>
					<button style="position: absolute;top: -100px;left: 40%;"  @click="startPick()">开始抽签！</button>
				</div>
				<label for="name-list">总人数</label>
				<input type="text" v-model="total" @input="changeTotal()" placeholder="输入人数"/>
				<br><label style="color: red;" for="name-list">如需修改在下方文本域进行，例如：有学生请假，直接把号数删除</label><br>
				
				<textarea  v-model="nameList" style="width: 300px;height: 200px;" ref="name-list" id="name-list"
					placeholder="" />
					<div  v-if="lucky">历史幸运儿：{{ lucky }}</div>
			</div>
			<div v-else>
				<div>
					<button style="position: absolute;top: -100px;left: 35%;"  @click="startPick2()">开始抽签！</button>
				</div>
				<label>请用英文逗号进行分割</label><br /><br>
				<textarea  v-model="custom" style="width: 300px;height: 200px;" ref="name-list" id="name-list"
					placeholder="" />
					<div  v-if="lucky2">历史幸运儿：{{ lucky2 }}</div>
			</div>
			
			
			
		</div>
		
		
	</div>
</template>

<script>
	export default {
		components: {},
		data() {
			return {
				pickedName: "",
				total: "",
				nameList: "",
				isChoose:true,
				custom:"",
				lucky:"",
				lucky2:""
			};
		},
		methods: {
			isTotal(){
				this.isChoose=true
			},
			isText(){
				this.isChoose=false
			},
			changeTotal(){
				this.nameList=""
				if(this.total>0&&this.total<100000){
					let i = 0
					for (i++; i < this.total; i++) {
						this.nameList = this.nameList + i + ","
					}
					this.nameList = this.nameList + i
				}
				else if(this.total==""){
					console.log()
				}
				else{
					alert("请输入1-99999数字")
				}
				
			},
			startPick() {
				if(this.total==""){
					alert("请输入1-99999数字")
				}else{
					let list = this.nameList.split(',');
					list = list.sort(() => {
						return Math.random() > 0.5 ? 1 : -1;
					});
					this.pickedName = list[0];
					this.lucky=this.lucky+this.pickedName+" "
					alert("恭喜你，"+this.pickedName)
				}
				
			},startPick2() {
				if(this.custom!=""){
					let list = this.custom.split(',');
					list = list.sort(() => {
						return Math.random() > 0.5 ? 1 : -1;
					});
					this.pickedName = list[0];
					this.lucky2=this.lucky2+this.pickedName+" "
					alert("恭喜你，"+this.pickedName)
				}else{
					alert("给文本域加点数据吧！")
				}
					
			},
		}
	};
</script>

<style lang="stylus">
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		width: 100vw;
		height: 100vh;
		display: flex;
		justify-content: space-around;
		align-items: center;
		flex-direction: column;
	}
</style>
