<template>
	<div class="high">
		<!-- header -->
		<header></header>
		<header class="clearFix hd">
			<i class="fl iconfont icon-tianjiayonghu"></i>
			<i class="fr iconfont icon-sousuo"></i>
			<div class="tabItem">
				<span class="topTab"
					v-for="(item,index) in tabNav"
					:key="index"
					@click="getContent(item.tip)"
					v-text="item.title"
					:class="item.tip === activeTitle ? 'tbActive' :''"
				></span>
			</div>
		</header>
		<!-- header -->

		<!-- content -->
		<div class="content">
			<div class="conlist recommend">
				<ul v-for="(item,index) in contentList" :key="index" 
                :style="index === activeTitle ? 'display: block;' : 'display: none;'">
					<li v-for="(item,index) in item" :key="index">
						<div class="userInfo clearFix">
							<p class="fl">
								<img :src="item.userHead" width="100%" height="100%" alt>
								<span v-text="item.userName"></span>
							</p>
							<i class="fr iconfont icon-ic_song_like"></i>
						</div>
						<div class="userShare">
							<mt-swipe :auto="0" class="shareImg">
								<mt-swipe-item v-for="(item,index) in item.userShare" :key="index">
									<img :src="item" width="100%" height="100%" v-preview="item" alt="" v-lazy="item">
								</mt-swipe-item>
							</mt-swipe>
						</div>
						<div class="tag clearFix">
							<p class="fl tbActive" v-text="'#'+item.userTag+'#'"></p>
							<i class="fr iconfont icon-liuyan"></i>
						</div>
					</li>
				</ul>
			</div>
			<!-- <div class="conlist findHot">
				<ul>
					<li v-for="(item,index) in findHot" :key="index">
						<div class="userInfo clearFix">
							<p class="fl">
								<img :src="item.userHead" width="100%" height="100%" alt>
								<span v-text="item.userName"></span>
							</p>
							<i class="fr iconfont icon-ic_song_like"></i>
						</div>
						<div class="userShare">
							<mt-swipe :auto="0" class="shareImg">
								<mt-swipe-item v-for="(item,index) in item.userShare" :key="index">
									<img :src="item" width="100%" height="100%" v-preview="item" alt="" v-lazy="item">
								</mt-swipe-item>
							</mt-swipe>
						</div>
						<div class="tag clearFix">
							<p class="fl tbActive" v-text="'#'+item.userTag+'#'"></p>
							<i class="fr iconfont icon-liuyan"></i>
						</div>
					</li>
				</ul>
			</div>
			<div class="conlist follow">
				<ul>
					<li v-for="(item,index) in follow" :key="index">
						<div class="userInfo clearFix">
							<p class="fl">
								<img :src="item.userHead" width="100%" height="100%" alt>
								<span v-text="item.userName"></span>
							</p>
							<i class="fr iconfont icon-ic_song_like"></i>
						</div>
						<div class="userShare">
							<mt-swipe :auto="0" class="shareImg">
								<mt-swipe-item v-for="(item,index) in item.userShare" :key="index">
									<img :src="item" width="100%" height="100%" v-preview="item" alt="" v-lazy="item">
								</mt-swipe-item>
							</mt-swipe>
						</div>
						<div class="tag clearFix">
							<p class="fl tbActive" v-text="'#'+item.userTag+'#'"></p>
							<i class="fr iconfont icon-liuyan"></i>
						</div>
					</li>
				</ul>
			</div> -->
		</div>
		<!-- content -->
	</div>
</template>

<script>
import connect from '../common/connect'
export default {
	data() {
		return {
            tabNav: [],
            activeTitle: 'recommend',
            contentList: {},
            // recommend: [],
            // findHot: [],
            // follow: []
		}
	},
	components: {},
	created() {
        {
            this.$ajax.get('findTabItem')
                .then(res => {
			        this.tabNav = res.data
            }).catch((err)=>{
                console.log(err);
            })
        }
        this.$ajax.get('contentList').then((res)=>{
                this.contentList = res.data;
                // console.log(this.contentList);
            })
        // this.getContent('recommend');
        connect.$emit('isIndex',true);
	},
	methods: {
        getContent(title){
            this.activeTitle = title;
        }

		// getContent(title) {
		// 	this.$ajax.get(title).then(res => {
        //         this[title] = res.data
        //         this.tabActive();
		// 	}).catch((err)=>{
        //         console.log(err);
        //     })
		// },
		// tabActive() {
        //     let $tabItem = this.$('.topTab')
        //     let $conlist = this.$('.conlist')
        //     for (let i = 0; i < $tabItem.length; i++) {
        //         $tabItem[i].index = i;
        //         $tabItem[i].onclick = function () {
        //             for (let i = 0; i < $tabItem.length; i++) {
        //                 $tabItem[i].className = '';
        //                 $conlist[i].style.display = 'none';
        //             }
        //             $tabItem[this.index].className = 'tbActive';
        //             $conlist[this.index].style.display = 'block';
        //         }
        //     }
            
        // }
	}
}
</script>

<style scoped lang="less">
@rem: 750/10rem;

.high {
	padding: 0 75/4 / @rem;
	header {
		height: 105 / @rem;
	}
	header.hd {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		height: 105 / @rem;
		line-height: 115 / @rem;
		padding: 0 75/4 / @rem;
		border-bottom: 1px solid #fafafa;
		font-size: 32 / @rem;
		background-color: white;
		z-index: 999;
		i {
			font-size: 42 / @rem;
		}
		i:first-of-type {
			margin-left: 15 / @rem;
		}
		i:last-of-type {
			margin-right: 15 / @rem;
		}
		span {
			margin: 0 10 / @rem;
		}
	}
	.content {
		width: 100%;
		margin-top: 20 / @rem;
		.conlist {
			// display: none;
			padding-bottom: 100 / @rem;
			ul li {
				width: 100%;
				border-radius: 10 / @rem;
				box-shadow: 0px 1px 10px #e8e6e9;
				margin-bottom: 25 / @rem;
				.userInfo {
					height: 100 / @rem;
					padding: 0 20 / @rem;
					line-height: 103 / @rem;
					p {
						// height: 100%;
						font-size: 0;
						img {
							width: 55 / @rem;
							height: 55 / @rem;
							border-radius: 50%;
							vertical-align: middle;
							transform: translateY(-5%);
						}
						span {
							margin-left: 20 / @rem;
							font-size: 34 / @rem;
							vertical-align: middle;
						}
					}
					i {
						font-size: 36 / @rem;
						font-weight: 600;
					}
				}
				.userShare {
					.shareImg {
						width: 100%;
						height: 450 / @rem;
					}
				}
				.tag {
					height: 100 / @rem;
					padding: 0 20 / @rem;
					line-height: 100 / @rem;
					p {
						font-size: 26 / @rem;
					}
					i {
						font-size: 38 / @rem;
						font-weight: 500;
					}
				}
			}
		}
		// .conlist.show {
		// 	display: block;
		// }
	}
}
</style>

