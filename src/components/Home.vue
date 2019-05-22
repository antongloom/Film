<template>
	<div class="content-wrapper">
		<section>
			<div class="container">
				<h1 class="ui-title-1">Home</h1>
				<input type="text" 
					   placeholder="What we will watch"
				       v-model="taskTitle"
				       @keyup.enter = "newTask">
				<textarea type="text"
					      v-model="taskDescription"
					      @keyup.enter = "newTask">
				</textarea>
				<div class="option-list">
					<input type="radio" 
						   class="what-watch--radio"
						   id="radioFilm"
						   value="Film"
						   v-model="whatWatch">
					<label for="radioFilm">Film</label>
					<input type="radio" 
						   class="what-watch--radio"
						   id="radioSerial"
						   value="Serial"
						   v-model="whatWatch">
					<label for="radioSerial">Serial</label>
				</div>
				<div class="total-time">
					<div class="total-time__film"
						 v-if="whatWatch === 'Film'">
						 <span class="time-title">Minutes</span>
						 <input class="time-input" 
						 		type="number">
					</div>
					<div class="total-time__serial"
						 v-if="whatWatch === 'Serial'">
						 <span>Total Serial Times</span>
					</div>
				</div>
				<div class="tag-list">
					<div class="ui-tag__wrapper">
  						<div class="ui-tag">
  							<span class="tag-title">Dogs</span>
  							<span class="button-close"></span>
  						</div>
					</div>
				</div>
			</div>
		</section>
	</div>
</template>
<script>
export default {
  	data(){		
  		return {
  		  taskTitle: '',
  		  taskDescription: '',
  		  whatWatch: '',
  		  tasksId: 3
  		}
  	},
  	methods: {
  		newTask(){
  			if(this.taskTitle === ''){
  				return
  			}
  			const task = {
  				id: this.taskId,
  				title: this.taskTitle,
  				description: this.taskDescription,	
  				whatWatch: this.whatWatch,
  				completed: false,	
				editing: false
  			}
  			console.log(task)

  			//Reset
  			this.taskId += 1
  			this.taskTitle = ''
  			this.taskDescription = ''
  		}
  	}
}
</script>
<style lang="stylus" scoped>
.option-list
	display flex
	align-items baseline
	.what-watch--radio
		margin-right 12px
	label
		margin-right 20px
		&:last-child
			margin-right 0px
</style>