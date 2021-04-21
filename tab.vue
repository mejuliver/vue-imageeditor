<template>
	<div class="tab-wrapper">
		<div class="tab-header">
			<ul>
				<li v-for="(item,index) in menu_data" :class="'tab-menu-item'+( item.active ? ' active' : '' )"><a href="#" @click.prevent="tabActivate(index)">{{ item.label }}</a></li>
			</ul>
		</div>
		<div class="tab-content" ref="tab-content">
			<slot></slot>
		</div>
	</div>
</template>

<style lang="scss" scoped>
	body.theme-dark{
		.tab-header{
			ul{
				li{
					a{
						background: none !important;
					}
					&.active a{
						border-color: #FFF!important;
					}
				}
			}
		}	
	}
	.tab .tab-header {
	  border-bottom: 1px solid #ccc;

	  ul {
	    margin: 0px;
	    padding: 0px;
	    width: 100%;
	    display: flex;
	    flex-direction: row;

	    li {
	      display: inline-flex;
	      align-items: center;
	      justify-content: center;
	      flex-basis: 50%;
	      flex-grow: 0;
	      border-bottom: 5px solid transparent;

	      &.active {
	        border-bottom-color: #09f !important;
	      }

	      a {
	        display: block;
	        text-decoration: none;
	        color: #252525;
	        padding: 16px 8px;
	        width: 100%;
	        text-align: center;
	      }

	      &:hover {
	        background: #ededed;
	      }
	    }
	  }
	}
	.tab-wrapper{
		.tab-header{
			ul{
				padding: 0px;
				margin: 0px;
				display: flex;
				li{
					display:flex;
					flex-grow: 1;
					flex-basis: 0;
					justify-content:center;
					align-items:center;
					border-bottom:1px solid #FFF;
					a{
						display:block;
						padding: 8px;
						border-bottom: 5px solid transparent;
						width: 100%;
						text-align:center;
						margin-bottom: -2px;
						text-decoration: none!important;
						background: #ededed;
					}
					a:hover{
						background: rgba(255,255,255,0.3);
					}
					&.active a{
						background: #ccc;
						border-bottom-color: #9c3532!important;
					}
				}
			}
		}
		.tab-content{
			.tab{
				color: #FFF;
				display:none;
				padding-top: 24px;
				padding-bottom: 24px;
				&.active{
					display:flex!important;
				}

			}
		}
	}
</style>

<script>
	export default{
		props : ['menu'],
		data(){
			return {
				menu_data : []
			}
		},
		watch : {
			menu_data(v){
				this.menu_data = v;
			}
		},
		computed : {},
		methods : {
			tabActivate(index){
				// set the active menu
				let q = this.menu_data.findIndex(i => i.active );

				if( q != -1 ){
					this.menu_data[q].active = false;
				}

				this.menu_data[index].active = true;

				if( this.$refs['tab-content'].querySelector('div.tab.active') ){
					this.$refs['tab-content'].querySelector('div.tab.active').classList.remove('active');
				}

				if( this.$refs['tab-content'].querySelectorAll('div.tab').length > 0 ){
					this.$refs['tab-content'].querySelectorAll('div.tab')[index].classList.add('active');
				}
			}
		},
		middleware : [],
		mounted(){
			this.menu_data = this.menu;

			// set menu active to content base on the index
			let q = this.menu_data.findIndex( i => i.active );
			if( q != -1 ){
				this.tabActivate(q);
			}
		},
		created(){}
	}
</script>