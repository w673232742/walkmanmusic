<template>
	<div class="header">
		<div class="icon"></div>
		<h1 class="txt">Wlakman Music</h1>
		<div class="mine">
			<i class="icon-mine"></i>
		</div>
	</div>
</template>

<script>
export default {
	
}	
</script>

<style lang="stylus" scoped>
	@import '~assets/styles/variable.styl'
	@import '~assets/styles/mixin.styl'
	.header
		position relative
		height 0.88rem
		text-align center
		color $color-theme
		.icon
			display inline-block
			vertical-align top
			width 0.6rem
			height 0.7rem
			bg-image('logo')
			background-size 0.6rem 0.7rem
			margin-top 0.1rem
			margin-right 0.1rem
		.txt
			display inline-block
			line-height 0.88rem
			font-size $font-size-large
		.mine
			position absolute
			top 0
			right 0
			.icon-mine
				display block
				padding .24rem
				font-size $font-size-large-x
				color $color-theme
</style>
