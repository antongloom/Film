<template>
	<div class="content-wrapper">
		<section>
			<div class="container">
				<div class="task-list">
					<div class="task-item"
						 v-for="task in tasks"
						 :key="task.id"
						 :class="{completed: task.completed}">
						 <div class="ui-card ui-card--shadow">
						 	<div class="task-item__info">
						 		<div class="task-item__main-info">
						 			<span class="ui-label ui-label--light">{{task.whatWatch}}</span>
							 		<span>Total Time:</span>
							 	</div>
							 	<span class="button-close"></span>	
						 	</div>
						 	<div class="task-item__content">
						 		<div class="task-item__header">
						 			<div class="ui-checkbox-wrapper">
							        <input class="ui-checkbox" 
							        	   type="checkbox"
							        	   v-model="task.completed">
							    	</div>
							 		<span class="ui-title-3">{{task.title}}</span>	
						 		</div>
						 		<div class="task-item__body">
						 			<p class="ui-text-regular">{{task.description}}</p>
						 		</div>
						 	</div>
						 </div> 	
					</div>
				</div>
			</div>
		</section>
	</div>
</template>
<script>
	export default{
		data(){
			return{
				tasks: [
					{
						'id': 1,
						'title': 'GrowthBusters: Hooked on Growth',
						'description': 'I directed this documentary challengi',
						'whatWatch': 'Film',
						'completed': false,
						'editing': false
					},
					{
						'id': 2,
						'title': 'Game of Thron',
						'description': 'Best serials',
						'whatWatch': 'Serial',
						'completed': false,	
						'editing': false
					}
				]
			}
		}
	}
</script>
<style lang="stylus" scoped>
.task-item
	margin-bottom 20px
	&:last-child
		margin-bottom 0px
.ui-label
	margin-right 8px
.task-item__info
	display flex
	align-items center
	justify-content space-between
	margin-bottom 20px
	.button-close
		width 20px
		height @width
.task-item__header
	display flex
	align-items center
	margin-bottom 18px
	.ui-checkbox-wrapper
		margin-right 8px
	.ui-title-3
		margin-bottom 0px	
</style>