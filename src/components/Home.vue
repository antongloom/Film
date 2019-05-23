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
					<!--Film Time-->
					<div class="total-time__film"
						 v-if="whatWatch === 'Film'">
						 <span class="time-title">Hours</span>
						 <input class="time-input" 
						 		type="number"
						 		v-model="filmHours">
						 <span class="time-title">Minutes</span>
						 <input class="time-input" 
						 		type="number"
						 		v-model="filmMinutes">
						<p>{{filmTime}}</p>
					</div>
					<!--Srial Time-->
					<div class="total-time__serial"
						 v-if="whatWatch === 'Serial'">
						 <span class="time-title">Howy many season?</span>
						 <input class="time-input" 
						 		type="number"
						 		v-model="serialSeason">
						 <span class="time-title">Howy many series?</span>
						 <input class="time-input" 
						 		type="number"
						 		v-model="serialSeries">
						 <span class="time-title">How long is one series? (minutes)</span>
						 <input class="time-input" 
						 		type="number"
						 		v-model="serialSeriesMinutes">
						 <p>{{serialTime}}</p>
					</div>
				</div>
				<!-- TAG LIST -->
				<!-- Add New Teg -->
				<div class="tag-list tag-list--add">
					<div class="ui-tag__wrapper"
						 @click="tagMenuShow = !tagMenuShow">
						 <div class="ui-tag">
						 	<span class="tag-title">Add New</span>
						 	<span class="button-close"
						 		  :class="{active : !tagMenuShow}">
						 	</span>
						 </div>
					</div>
				</div>
				<!-- Show Input -->
				<div class="tag-list tag-list--menu"
					 v-if="tagMenuShow">
					 	<input class="tag-list tag-list-menu" 
					 		   type="text"
					 		   placeholder="New teg"
					 		   v-model="tagTitle"
					 		   @keyup.enter="newTeg">
					    <div class="button button-default"
					    	 @click="newTeg">Send</div>	
					 </div>
				<div class="tag-list">
					<div class="ui-tag__wrapper"
						 v-for="tag in tags"
						 :key="tag.title">
  						<div class="ui-tag"
  							 @click="addTagUsed(tag)"
  							 :class="{active: tag.use}">
  							<span class="tag-title">{{tag.title}}</span>
  							<span class="button-close"></span>
  						</div>
					</div>
					<p>{{tagsUsed}}</p>
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
  		  tasksId: 3,
  		  filmHours: 1,
  		  filmMinutes: 30,
  		  serialSeason: 1,
  		  serialSeries: 11,
  		  serialSeriesMinutes: 40,
  		  tagTitle: '',
  		  tagMenuShow: false,
  		  tagsUsed: [],
  		  tags: [
  		  	{
  		  		title: 'Comedy',
  		  		use: false
  		  	},
  		  	{
  		  		title: 'Westerns',
  		  		use: false
  		  	},
  		  	{
  		  		title: 'Adventure',
  		  		use: false
  		  	},
  		  ]
  		}
  	},
  	methods: {
  		newTeg(){
  			if(this.tagTitle === ''){
  				return
  			}
  			this.tags.push({
  				title: this.tagTitle,
  				used: false
  			})
  			/*const tag = {
  				title: this.tagTitle
  			} */
  		},
  		newTask(){
  			if(this.taskTitle === ''){
  				return
  			}
  			let time
  			if(this.whatWatch === 'Film'){
  				time = this.filmTime	
  			}else{
  				time = this.serialTime
  			}
  			const task = {
  				id: this.taskId,
  				title: this.taskTitle,
  				description: this.taskDescription,	
  				whatWatch: this.whatWatch,
  				time,
  				completed: false,	
				editing: false
  			}
  			console.log(task)

  			//Reset
  			this.taskId += 1
  			this.taskTitle = ''
  			this.taskDescription = ''
  		},
  		addTagUsed(tag){
  			tag.use = !tag.use
  			if (tag.use){
  				this.tagsUsed.push(
  					tag.title
  				)
  			}else{
  				this.tagsUsed.splice(tag.title, 1)
  			}
  		},
  		getHoursAndMinutes(minutes){		
  			let hours = Math.trunc(minutes / 60)
  			let min = minutes % 60
  			return hours + ' Hours ' + min + ' Minutes '
  		}
  	},
  	computed: {
  		filmTime(){
  			let min = (this.filmHours * 60) + (this.filmMinutes * 1)
  			return this.getHoursAndMinutes(min)
  		},
  		serialTime(){
  			let min = this.serialSeason * this.serialSeries * this.serialSeriesMinutes
  			return this.getHoursAndMinutes(min)
  		}
  	}
}
</script>
<style lang="stylus" scoped>
<style lang="stylus" scoped>
// Options
.option-list
  display flex
  align-items center
  margin-bottom 20px
  .what-watch--radio
    margin-right 12px
  input
    margin-bottom 0
  label
    margin-right 20px
    margin-bottom 0
    &:last-child
      margin-right 0
// Total time
.total-time
  margin-bottom 20px
.time-title
  display block
  margin-bottom 6px
.time-input
  max-width 80px
  margin-right 10px
// Tags
.tag-list
  margin-bottom 20px
.ui-tag__wrapper
  margin-right 18px
  margin-bottom 10px
  &:last-child
    margin-right 0
.ui-tag
  .button-close
    &.active
      transform: rotate(45deg)
  &.used
    background-color: #444ce0
    color #fff
    .button-close
      &:before,
      &:after
        background-color: #fff
// Tag Menu Show
.tag-list--menu
  display flex
  justify-content space-between
  align-items center
// New Tag Input
.tag-add--input
  margin-bottom 0
  margin-right 10px
  height 42px
// Total Time
.total-time
  p
    margin-bottom 6px
  span
    margin-right 16px
  .task-input
    max-width 80px
    margin-bottom 28px
    margin-right 10px
.button-list
  display flex
  justify-content flex-end
</style>