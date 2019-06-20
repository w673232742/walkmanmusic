<template>
	<div ref="wrapper" class="wrapper">
		<div>
			<mt-loadmore ref="loadmore" :top-method="loadTop" @top-status-change="handleTopChange">
				<mt-swipe :auto="4000">
				<mt-swipe-item v-for='item in swiperList' :key='item.id'>
					<img :src="item.picUrl">
				</mt-swipe-item>
				</mt-swipe>
				<div class="song_order">
					<div class="hot_txt">
						<h2>热门歌单推荐</h2>
					</div>
					<div class="song_list" v-for="item in songList" :key='item.id'>
						<div class="list_img">
							<img :src="item.picUrl" />
						</div>
						<div class="list_txt">
							<h3 v-text="item.songListAuthor"></h3>
							<p v-text="item.songListDesc"></p>
						</div>
					</div>
				</div>
				<div slot="top" class="mint-loadmore-top">
					<span v-show="topStatus !== 'loading'" :class="{ 'rotate': topStatus === 'drop' }">↓</span>
					<span v-show="topStatus === 'loading'">Loading...</span>
				</div>
			</mt-loadmore>
		</div>
	</div>
</template>

<script>
import axios from 'axios'
import BScroll from 'better-scroll'

export default {
	data:function(){
		return {
			swiperList:[],
			songList:[],
			topStatus:''
		}
	},
	methods:{
		loadTop(){
			this.loadeMsg();
			this.$refs.loadmore.onTopLoaded();
		},
		handleTopChange(status){
			this.topStatus=status;
		},
		loadeMsg(){
			axios.get('/api/musichall/fcgi-bin/fcg_yqqhomepagerecommend.fcg',{
				params:{
					_: 1560183655241,
					g_tk: 5381,
					uin: 0,
					format: 'json',
					inCharset: 'utf-8',
					outCharset: 'utf-8',
					notice: 0,
					platform: 'h5',
					needNewCode: 1,
				}
			})
			.then(res=>{
				// console.log(res.data.data.songList);
				this.swiperList=res.data.data.slider;
				this.songList=res.data.data.songList;
			})
			.catch(err=>{
				console.log(err);
			})
		}
	},
	created() {
		this.loadeMsg();
	},
	mounted(){
		this.scroll=new BScroll(this.$refs.wrapper)
	},
}
</script>

<style lang="stylus" scoped>
@import '~assets/styles/variable.styl'
.wrapper
	overflow hidden
	position absolute
	top 1.8rem
	left 0
	right 0
	bottom 0
	.mint-swipe
		overflow hidden
		padding-bottom 40%
		width 100%
		height 0
		.mint-swipe-items-wrap
			width 100%
			height 100%
			.mint-swipe-item
				width 100%
				height 100%
				img
					width 100%
	.song_order
		.hot_txt
			width 100%
			height 1.4rem
			h2
				text-align center
				line-height 1.4rem
				font-size $font-size-medium-x
				color $color-theme
		.song_list
			display flex
			padding .2rem .3rem
			align-items center
			.list_img
				width 20%
				img
					width 100%
					height 100%
			.list_txt
				align-items center
				overflow hidden
				margin-left .4rem
				h3
					font-size $font-size-medium
					padding-bottom .3rem
				p
					color $color-text-l
					font-size $font-size-medium
					white-space nowrap
					text-overflow ellipsis
					overflow hidden
</style>