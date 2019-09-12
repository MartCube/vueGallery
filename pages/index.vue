<template>
	<div class="container">
		<div class="gallery">
			<vueLightbox :thumbnails="lightbox.thumbnails" :images="lightbox.images" :thumbnail-path="lightbox.thumbnailPath" :image-path="lightbox.imagePath" />
		</div>
	</div>
</template>

<script>
import vueLightbox from '~/components/vue-lightbox.vue'

export default {
	components: {
		vueLightbox,
	},
	data() {
		return {
			lightbox: {
				thumbnails: ['1s.jpg', '2s.jpg', '3s.jpg', '4s.jpg', '5s.jpg', '6s.jpg', '7s.jpg', '8s.jpg', '9s.jpg', '10s.jpg', '11s.jpg', '12s.jpg'],
				images: ['1.jpg', '2.jpg', '3.jpg', '4.jpg', '5.jpg', '6.jpg', '7.jpg', '8.jpg', '9.jpg', '10.jpg', '11.jpg', '12.jpg'],
				thumbnailPath: '/thumbnails/',
				imagePath: '/photos/',
			},
		}
	},
}
</script>

<style lang="scss" scoped>
.container {
	justify-content: flex-start;
}
.gallery {
	max-width: 1000px;
	text-align: center;

	display: flex;
	justify-content: center;
	align-items: center;
	align-content: center;
	flex-wrap: wrap;
}
</style>
