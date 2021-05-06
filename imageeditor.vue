<template>
  <div class="imageeditor_wrapper">
  	<input type="file" :name="inputname" :accept="inputaccept" :value="inputvalue" :placeholder="inputplaceholder" :class="inputclass" @change="openImageEditor()">
    <div :class="'justmodal-shadow '+( modal_open ? 'active' : '' )"></div>
    <div :class="'justmodal-wrapper '+( modal_open ? 'active' : '' )">
      <div class="justmodal-container">
        <i class="fa fa-times justmodal-close" @click="modal_open=false"></i>
        <div class="justmodal-content mt16">
          <div class="row">
            <div class="col-12 col-md-12 col-lg-12 col-12">
              	<div class="row">
					<div class="col-12">
						<div class="cropper-view">
							<cropper
								:src="img"
								@change="change"
							/>
						</div>
					</div>
					<div class="col-12">
						<div class="row mt16">
							<div class="col-4">
								<div class="preview_wrapper">
									<div>
										<img :src="img2" alt="" ref="preview_img" id="preview_img" class="preview" v-show="!effect">
										<div id="canvas_container" ref="canvas_container" v-show="effect"></div>
									</div>
								</div>
							</div>
							<div class="col-8">
								<div class="row">
									<div class="col-12">
										<tab :menu="[
											{ label : 'Filters', value : 'filters', active : true, visibility : true },
											{ label : 'Effects', value : 'effects', active : false, visibility : true }
										]">
											<div class="tab row">
												<div class="col-6 mb16">
													<p class="mb8"><b>Brightness</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="brightness">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Vibrance</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="vibrance">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Contrast</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="contrast">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Saturation</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="saturation">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Exposure</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="exposure">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Sepia</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="sepia">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Noise</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="noise">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Sharpen</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="sharpen">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Hue</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="hue">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Gamma</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="gamma">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>Clip</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="clip">
												</div>
												<div class="col-6 mb16">
													<p class="mb8"><b>StackBlur</b></p>
													<input type="range" min="-10" max="10" value="0" class="slider" @change="camanFilter()" data-filter="stackblur">
												</div>
											</div>
											<div class="tab row">
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter>Vintage</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="lomo">Lomo</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="clarity">Clarity</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="sinCity">Sin City</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="sunrise">Sunrise</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="crossProcess">Cross Process</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="orangePeel">Orange Peel</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="love">Love</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="grungy">Grungy</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="jarques">Jarques</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="pinhole">Pinhole</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="OldBoot">Old Boot</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="glowingSun">Glowing Sun</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="hazyDays">hazyDays</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="herMajesty">Her Majesty</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="nostalgia">Nostalgia</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="hemingway">Hemingway</a>
												</div>
												<div class="col-4 mb16">
													<a class="btn btn-success btn-primary btn-block" @click.prevent="camanEffects()" data-filter="concentrate">Concentrate</a>
												</div>
											</div>
										</tab>
									</div>
								</div>
								<div class="row">
									<div class="col-12">
										<a class="btn btn-primary m2 c-white" @click="saveImage()">Save</a><a class="btn m2" @click="resetFilter()">Reset</a>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
	body.theme-dark{
		.slider {
		  background: none!important;
		}

		.slider::-webkit-slider-thumb {
		  background: #FFF!important;
		}

		.slider::-moz-range-thumb {
		  background: #FFF!important;
		}
	}

	.slider{
		width: 100%;
	}
	.imageeditor_wrapper{
		position:relative;
		overflow: hidden;
		.cropper-view{
			width:100%;
			height:100%;
		}
		.preview_wrapper{
			display:flex;
			align-items: center;
			justify-content: center;
			border:1px solid #ccc;
			.preview{
				max-width: 100%;
				max-height: 100%;
			}
		}
	}
	// modal
	.justmodal-shadow {
		position: fixed;
		top: 0px;
		left: 0px;
		width: 100%;
		height: 100vh;
		background: rgba(0,0,0,0.5);
		z-index: 9999;
		display: none;
	}
	.justmodal-shadow.active {
		display: block !important;
	}
	.justmodal-wrapper {
		position: fixed;
		width: 100%;
		height: 100vh;
		z-index: -999;
		top: 0px;
		left: 0px;
		align-items: center;
		justify-content: center;
		display: flex !important;
		opacity: 0;
		transition: all 0.3s ease;
		-webkit-transition: all 0.3s ease;
		-moz-transition: all 0.3s ease;
		transform: translate3d(0, 10px, 0);
		-webkit-transform: translate3d(0, 10px, 0);
		-moz-transform: translate3d(0, 10px, 0);
		visibility: hidden;
	}
	.justmodal-wrapper.active {
		z-index: 99999 !important;
		opacity: 1 !important;
		transform: translate3d(0, 0px, 0) !important;
		-webkit-transform: translate3d(0, 0px, 0) !important;
		-moz-transform: translate3d(0, 0px, 0) !important;
		visibility: visible !important;
	}
	.justmodal-container {
		min-height: 60px;
		max-height: 100%;
		background: #FFF;
		width: 80%;
		padding: 24px 0px;
		position: relative;
		-webkit-box-shadow: 0 10px 40px -6px rgba(0,0,0,.1);
		-moz-box-shadow: 0 10px 40px -6px rgba(0,0,0,.1);
		-o-box-shadow: 0 10px 40px -6px rgba(0,0,0,.1);
		box-shadow: 0 10px 40px -6px rgba(0,0,0,.1);
		.justmodal-header {
			padding: 0px 24px 8px 24px;
			border-bottom: 1px solid #ededed;
			margin-bottom: 24px;
			h3 {
				margin-top: 0px !important;
				margin-bottom: 0px !important;
			}
		}
		.justmodal-content {
			padding: 0px 24px;
			max-height: 87vh;
			overflow-y: auto;
		}
	}
	.justmodal-close {
		position: absolute;
		top: 16px;
		right: 16px;
		font-size: 16px;
		z-index: 10;
		opacity: .5;
		color: #555;
		cursor: pointer;
		&:hover {
		  opacity: 1 !important;
		}
	}
	@media (max-width: 767px ) {
		.justmodal-container {
		  width: 90% !important;
		}
		#app-loader-content {
		  width: 95% !important;
		}
	}
	@media (min-width: 768px ) and (max-width: 1024px ) {
		.justmodal-container {
		  width: 500px !important;
		}
	}

	// slider
	.slider {
	  -webkit-appearance: none;
	  width: 100%;
	  height: 7px;
	  background: #d3d3d3;
	  outline: none;
	  opacity: 0.7;
	  -webkit-transition: .2s;
	  transition: opacity .2s;
	  border-radius: 20px;
	}

	.slider:hover {
	  opacity: 1;
	}

	.slider::-webkit-slider-thumb {
	  -webkit-appearance: none;
	  appearance: none;
	  width: 15px;
	  height: 15px;
	  background: #9c3532;
	  cursor: pointer;
	  border-radius: 50%;
	}

	.slider::-moz-range-thumb {
	  width: 15px;
	  height: 15px;
	  background: #9c3532;
	  cursor: pointer;
	  border-radius: 50%;
	}
</style>

<script>
	import { Cropper } from 'vue-advanced-cropper';
	import 'vue-advanced-cropper/dist/style.css';
	import tab from './tab.vue';

	export default{
		props : [ 'inputname', 'inputaccept', 'inputvalue', 'inputplaceholder', 'inputclass' ],
		data(){
			return {
				img: '',
				img2 : '',
				is_ready : 1,
				modal_open : false,
				effect : false,
				file_attr : {
					name : '',
					ext : ''
				}
			}
		},
		components : { Cropper, tab },
		watch : {
			is_ready(v){
				this.is_ready = v;
			}
		},
		computed : {},
		methods : {
			base64toBlob(base64Data, contentType) {
			    contentType = contentType || '';
			    var sliceSize = 1024;
			    var byteCharacters = atob(base64Data);
			    var bytesLength = byteCharacters.length;
			    var slicesCount = Math.ceil(bytesLength / sliceSize);
			    var byteArrays = new Array(slicesCount);

			    for (var sliceIndex = 0; sliceIndex < slicesCount; ++sliceIndex) {
			        var begin = sliceIndex * sliceSize;
			        var end = Math.min(begin + sliceSize, bytesLength);

			        var bytes = new Array(end - begin);
			        for (var offset = begin, i = 0; offset < end; ++i, ++offset) {
			            bytes[i] = byteCharacters[offset].charCodeAt(0);
			        }
			        byteArrays[sliceIndex] = new Uint8Array(bytes);
			    }
			    return new Blob(byteArrays, { type: contentType });
			},
			saveImage(){

				let img = this.img2;

				if( this.$refs.canvas_container.querySelector('img') ){
					img = this.$refs.canvas_container.querySelector('img').getAttribute('src');
				}else if( this.$refs.canvas_container.querySelector('canvas') ){
					img = this.$refs.canvas_container.querySelector('canvas').toDataURL("image/jpeg");
				}

				let blob = this.base64toBlob(img.split(',').pop(),'image/'+this.file_attr.ext);

				this.img = '';
				this.img2 = '';

				this.$emit('saveImage', { blob : blob, src : img } );

				this.modal_open = false;
			},
			openImageEditor(){

				this.file_attr = {
					name : event.target.value.split('\\').pop(),
					ext : event.target.value.split('.').pop()
				}

				if( event.target.value == '' ){
					return;
				}


				let _this = this
				let fr = new FileReader();
	            fr.onloadend = function(){
	            	_this.img = fr.result;
	            	_this.modal_open = true;
	            }
	            fr.readAsDataURL(event.target.files[0]);
			},
			resetFilter(){
				this.effect = false;
			},
			camanEffects(){

				let canvas = false;

				if( this.$refs.canvas_container.querySelector('canvas') ){
					canvas = this.$refs.canvas_container.querySelector('canvas');
				}
				
				let el = document.createElement('img');
				
				el.src = canvas ? canvas.toDataURL() : this.img2;

				if( canvas ){
					canvas.remove();
				}

				if( this.$refs.canvas_container.querySelector('img') ){
					this.$refs.canvas_container.querySelector('img').remove();
				}

				this.$refs.canvas_container.appendChild(el);

				this.effect = true;

				let slider = event.target;
				let t = slider.getAttribute('data-filter');
				let v = slider.value;

				if( v == 50 ){
					v = 0;
				}

				Caman('#canvas_container img', function () {

					switch(t){
						case 'vintage':
							this.vintage().render();
						break;
						case 'lomo':
							this.lomo().render();
						break;
						case 'clarity':
							this.clarity().render();
						break;
						case 'sinCity':
							this.sinCity().render();
						break;
						case 'sunrise':
							this.sunrise().render();
						break;
						case 'crossProcess':
							this.crossProcess().render();
						break;
						case 'orangePeel':
							this.orangePeel().render();
						break;
						case 'love':
							this.love().render();
						break;
						case 'grungy':
							this.grungy().render();
						break;
						case 'jarques':
							this.jarques().render();
						break;
						case 'pinhole':
							this.pinhole().render();
						break;
						case 'oldBoot':
							this.oldBoot().render();
						break;
						case 'glowingSun':
							this.glowingSun().render();
						break;
						case 'hazyDays':
							this.hazyDays().render();
						break;
						case 'herMajesty':
							this.herMajesty().render();
						break;
						case 'nostalgia':
							this.nostalgia().render();
						break;
						case 'hemingway':
							this.hemingway().render();
						break;
						case 'concentrate':
							this.concentrate().render();
						break;
					}
				});
			},
			camanFilter(){

				let canvas = false;

				if( this.$refs.canvas_container.querySelector('canvas') ){
					canvas = this.$refs.canvas_container.querySelector('canvas');
				}
				
				let el = document.createElement('img');
				
				el.src = canvas ? canvas.toDataURL() : this.img2;

				if( canvas ){
					canvas.remove();
				}

				if( this.$refs.canvas_container.querySelector('img') ){
					this.$refs.canvas_container.querySelector('img').remove();
				}

				this.$refs.canvas_container.appendChild(el);
				

				this.effect = true;

				let slider = event.target;
				let t = slider.getAttribute('data-filter');
				let v = slider.value;

				if( v == 50 ){
					v = 0;
				}

				console.log( v );

				Caman(el, function () {
					switch( t ){
						case 'brightness':
							this.brightness(v);
						break;
						case 'vibrance':
							this.vibrance(v);
						break;
						case 'hue':
							this.hue(v);
						break;
						case 'gamma':
							this.gamma(v);
						break;
						case 'clip':
							this.clip(v);
						break;
						case 'stackblur':
							this.stackBlur(v);
						break;
						case 'contrast':
							this.contrast(v);
						break;
						case 'saturation':
							this.saturation(v);
						break;
						case 'exposure':
							this.exposure(v);
						break;
						case 'sepia':
							this.sepia(v);
						break;
						case 'noise':
							this.noise(v);
						break;
						case 'sharpen':
							this.sharpen(v);
						break;
					}

					this.render();
				});
			},
			change({ coordinates, canvas }) {

				this.img2 = canvas.toDataURL();

				if( this.$refs.canvas_container.querySelector('canvas') ){
					this.$refs.canvas_container.querySelector('canvas').remove();
				}

				let el = document.createElement('img');
				el.src=this.img2

				if( this.$refs.canvas_container.querySelector('img') ){
					this.$refs.canvas_container.querySelector('img').remove();
				}

				this.$refs.canvas_container.appendChild(el);

			},
			loadScript(src,callback){
				var s,
	                r,
	                t;
	                r = false;
	                s = document.createElement('script');
	                s.type = 'text/javascript';
	                s.src = src;
	                s.crossorigin="anonymous";
	                s.onload = s.onreadystatechange = function() {
	                //console.log( this.readyState ); //uncomment this line to see which ready states are called.
	                if ( !r && (!this.readyState || this.readyState == 'complete') ){
	                  r = true;
	                  if( typeof callback == 'function' ){
	                    callback();
	                  }
	                }
	            };
	            t = document.getElementsByTagName('script')[0];
	            t.parentNode.insertBefore(s, t);
			}
		},
		mounted(){},
		created(){
			let _this = this;

			this.loadScript('https://cdnjs.cloudflare.com/ajax/libs/camanjs/4.0.0/caman.full.min.js',()=>{
				_this.is_ready = _this.is_ready - 1;
			});
		}
	}
</script>