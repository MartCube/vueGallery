<template>
	<div class="thumb_container">
		<div v-for="(thumbnail, index) in thumbnails" :key="thumbnail" class="thumbnail" @click="Toggle(index)">
			<img :src="thumbnailPath + thumbnail" />
			<div class="plus">
				<i class="icon icon-plus" />
			</div>
			<div class="color-overlay"></div>
		</div>

		<transition name="fade" mode="out-in">
			<div v-if="visible" class="lightbox">
				<i class="icon-cancel" @click="Toggle()" />
				<i class="icon-left" @click="Prev()" />
				<i class="icon-right" @click="Next()" />
				<transition name="fade" mode="out-in">
					<img :key="currentImage" :src="imagePath + [currentImage + 1] + '.jpg'" />
				</transition>
			</div>
		</transition>
	</div>
</template>

<script>
export default {
	props: {
		thumbnails: {
			type: Array,
			required: true,
		},
		images: {
			type: Array,
			required: true,
		},
		thumbnailPath: {
			type: String,
			required: true,
		},
		imagePath: {
			type: String,
			required: true,
		},
	},
	data() {
		return {
			visible: false,
			currentImage: 0,
		}
	},
	mounted() {
		window.addEventListener('keydown', this.onKeydown)
	},
	destroyed() {
		window.removeEventListener('keydown', this.onKeydown)
	},
	methods: {
		Toggle(index) {
			this.currentImage = index
			this.visible = !this.visible
		},
		Next() {
			if (this.currentImage < this.images.length - 1) {
				this.currentImage++
			} else {
				this.currentImage = 0
			}
		},
		Prev() {
			if (this.currentImage > 0) {
				this.currentImage--
			} else {
				this.currentImage = this.images.length - 1
			}
		},
		onKeydown(e) {
			if (this.visible) {
				switch (e.key) {
					case 'ArrowRight':
						this.Next()
						break
					case 'ArrowLeft':
						this.Prev()
						break
					case 'Escape':
						this.Toggle()
						break
				}
			}
		},
	},
}
</script>

<style lang="scss" scoped>
$transition: all 0.35s cubic-bezier(0.31, -0.105, 0.43, 1.59);

.thumb_container {
	display: flex;
	justify-content: center;
	align-items: center;
	align-content: center;
	flex-wrap: wrap;
}

.thumbnail {
	position: relative;
	max-width: 300px;
	height: 300px;
	margin: 10px;
	cursor: pointer;

	display: flex;
	justify-content: center;
	align-items: center;
	align-content: center;

	img {
		max-width: 300px;
		border-radius: 10px;
	}
	.color-overlay {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		border-radius: 10px;
		background: rgba(0, 0, 0, 0.5);
		opacity: 0.2;
		transition: $transition;
	}
	.plus {
		position: absolute;
		width: 50px;
		height: 50px;
		line-height: 45px;
		border: #fc4a1a 3px solid;
		border-radius: 50%;
		text-align: center;

		z-index: 2;
		transform: scale(0.5);
		opacity: 0;
		transition: $transition;
		i {
			color: white;
			font-size: 1.5em;
		}
	}

	&:hover {
		.color-overlay {
			opacity: 1;
		}
		.plus {
			opacity: 1;
			transform: scale(1);
		}
	}
}

.lightbox {
	display: flex;
	justify-content: center;
	align-items: center;

	z-index: 999;
	position: fixed;
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	background: rgba(0, 0, 0, 0.85);

	img {
		max-width: 90%;
		max-height: 90%;
	}

	i {
		opacity: 0.5;
	}
	.icon-cancel {
		cursor: pointer;
		font-size: 40px;
		color: white;

		position: fixed;
		top: 0;
		right: 0;
		margin: 10px;

		transition: $transition;
		&:hover {
			transform: scale(1.1);
			opacity: 0.9;
		}
	}
	.icon-left {
		cursor: pointer;
		font-size: 50px;
		color: white;

		position: fixed;
		top: 50;
		left: 0;
		padding: 10px;

		transition: $transition;
		&:hover {
			transform: scale(1.1);
			opacity: 0.9;
		}
	}
	.icon-right {
		cursor: pointer;
		font-size: 50px;
		color: white;

		position: fixed;
		top: 50;
		right: 0;
		padding: 10px;

		transition: $transition;
		&:hover {
			transform: scale(1.1);
			opacity: 0.9;
		}
	}
}

.fade-enter-active,
.fade-leave-active {
	transition: $transition;
}
.fade-enter,
.fade-leave-to {
	opacity: 0;
}
</style>
