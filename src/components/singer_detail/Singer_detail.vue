<template>
	<div class="music_list">
			<div class="back"><i class="icon-back"></i></div>
			<h3 class="title">薛之谦</h3>
			<div>
				<i></i>
				<span></span>
			</div>
		</div>
</template>

<script>
export default {
	
}
</script>

<style lang="stylus" scoped>
@import '~assets/styles/variable.styl'
.music_list
	position fixed
	z-index 100
	top 0
	left 0
	right 0
	bottom 0
	background $color-background
	.back
		
		.icon-back
			display inline-block
			position absolute
			top .2rem
			left .3rem
			font-size $font-size-large-x
			color $color-theme
			height 1rem
			width 1rem
		.title
			text-align center
			font-size $font-size-large
</style>
