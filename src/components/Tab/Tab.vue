<template>
	<div class="nav">
		<router-link class="nav-item" tag='div' to='/home'><span>推荐</span></router-link>
		<router-link class="nav-item" tag='div' to='/Singer'><span>歌手</span></router-link>
		<router-link class="nav-item" tag='div' to='/Rank'><span>排行</span></router-link>
		<router-link class="nav-item" tag='div' to='/Search'><span>搜索</span></router-link>
	</div>
</template>

<script>
export default {
	
}
</script>

<style lang="stylus" scoped>
@import "~assets/styles/variable.styl"
.nav
	display flex
	height 0.88rem
	line-height 0.88rem
	font-size $font-size-medium-x
	.nav-item
		flex 1
		text-align center
		span
			color $color-text-l
			padding-bottom .1rem
		&.router-link-active
			span
				color $color-theme
				border-bottom 0.04rem solid $color-theme
</style>
