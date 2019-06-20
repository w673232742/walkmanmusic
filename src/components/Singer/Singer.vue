<template>
	<div>
		<mt-index-list>
			<mt-index-section v-for="val in singerList" :index="val.str" :key='val.index'>
				<mt-cell v-for="item in val.singerlist" :key="item.mid">
					<router-link to="Singer/detail">
						<img :src="item.singer_pic" />
						{{item.singer_name}}
					</router-link>
				</mt-cell>
			</mt-index-section>
		</mt-index-list>
		<router-view></router-view>
	</div>
</template>

<script>
import axios from 'axios'
import { Indicator } from 'mint-ui';
export default {
	data(){
		return {
			sortSinger:[],
			singerList:[],
			indexList:[]
		}
	},
	created(){
		Indicator.open('加载中...');
		axios.get('/apitwo/cgi-bin/musicu.fcg',{
			params:{
				'-': 'getUCGI797519194630409',
				g_tk: 1539167653,
				loginUin: 0,
				hostUin: 0,
				format: 'json',
				inCharset: 'utf8',
				outCharset: 'utf-8',
				notice: 0,
				platform: 'yqq.json',
				needNewCode: 0,
				data: {"comm":{"ct":24,"cv":0},"singerList":{"module":"Music.SingerListServer","method":"get_singer_list","param":{"area":-100,"sex":-100,"genre":-100,"index":-100,"sin":0,"cur_page":1}}}
			}
		})
		.then(res=>{
			// console.log(res);
			this.indexList=res.data.singerList.data.tags.index;
			for(let i=0;i<this.indexList.length;i++){
				axios.get('/apitwo/cgi-bin/musicu.fcg',{
					params:{
						'-': 'getUCGI797519194630409',
						g_tk: 1539167653,
						loginUin: 0,
						hostUin: 0,
						format: 'json',
						inCharset: 'utf8',
						outCharset: 'utf-8',
						notice: 0,
						platform: 'yqq.json',
						needNewCode: 0,
						data: {"comm":{"ct":24,"cv":0},"singerList":{"module":"Music.SingerListServer","method":"get_singer_list","param":{"area":-100,"sex":-100,"genre":-100,"index":this.indexList[i].id,"sin":0,"cur_page":1}}}
					}
				})
				.then(res=>{
					// this.sortSinger.push(res)
					// console.log(res.data.singerList.data);
					if(res.data.singerList.data.index== -100){
						this.sortSinger.push({
							index:res.data.singerList.data.index,
							str:'hot',
							singerlist:res.data.singerList.data.singerlist.slice(0,10)
						})
					}else if(res.data.singerList.data.index== 27){
						this.sortSinger.push({
							index:res.data.singerList.data.index,
							str:'#',
							singerlist:res.data.singerList.data.singerlist.slice(0,10)
						})
					}else{
						this.sortSinger.push({
							index:res.data.singerList.data.index,
							str:String.fromCharCode(res.data.singerList.data.index+64),
							singerlist:res.data.singerList.data.singerlist.slice(0,10)
						})
					}
					// console.log(this.indexList.length);
					if(i==this.indexList.length-1){
						Indicator.close();
						function sortNumber(a,b){
							return a.index-b.index;
						}
						this.singerList=this.sortSinger.sort(sortNumber)
					}
				})
				.catch(err=>{
					console.log(err);
				})
			}
		})
		.catch(err=>{
			console.log(err);
		})
	}
}
</script>

<style lang="stylus" scoped>
	
</style>
