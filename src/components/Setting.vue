<template>
	<div class="setting">
		<div class="setting__head">
			<h3>Clock Sound</h3>
		</div>
		<div class="setting__wrap">
			<div class="setting__wrap__item">
				<div
					class="setting__wrap__item__input"
					@click="nowSound = 'sound_1'">
					<div
						v-if="nowSound === 'sound_1'"
						class="active"></div>
				</div>
				<div class="setting__wrap__item__text">Sound 1</div>
			</div>
			<div class="setting__wrap__item">
				<div
					class="setting__wrap__item__input"
					@click="nowSound = 'sound_2'">
					<div
						v-if="nowSound === 'sound_2'"
						class="active"></div>
				</div>
				<div class="setting__wrap__item__text">Sound 2</div>
			</div>
			<div class="setting__wrap__item">
				<div
					class="setting__wrap__item__input"
					@click="nowSound = 'sound_3'">
					<div
						v-if="nowSound === 'sound_3'"
						class="active"></div>
				</div>
				<div class="setting__wrap__item__text">Sound 3</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			nowSound: 'sound_1'
		}
	}
}
</script>
<style lang="sass" scoped>
@font-face
  font-family: TaipeiSansTCBeta-Bold
  src: url('/src/fonts/TaipeiSansTCBeta-Bold.ttf')

@font-face
  font-family: TaipeiSansTCBeta-Light
  src: url('/src/fonts/TaipeiSansTCBeta-Light.ttf')

@font-face
  font-family: TaipeiSansTCBeta-Regular
  src: url('/src/fonts/TaipeiSansTCBeta-Regular.ttf')

$white: #FFFFFF;
$black: #000000;
$red: #BA000D;
$tomatoRed: #F44336;
$gray: #707070;
$darkGray: #6A6868;
.setting
	max-width: 525px
	width: 100%
	margin: 0 auto
	font-family: 'TaipeiSansTCBeta-Regular'
	padding: 0 24px

	&__head
		width: calc(100% - 48px)
		height: 35px
		background-color: $black
		color: $white
		padding: 0 24px
		display: flex
		align-items: center
		position: relative
		margin-top: 28px

	&__wrap
		display: flex
		flex-wrap: wrap
		margin-top: 20px
		&__item
			width: calc(50% - 48px)
			display: flex
			align-items: center
			margin: 20px 0
			padding: 0 24px

			&__input
				display: flex
				align-items: center
				justify-content: center
				width: 20px
				height: 20px
				border: 2px solid
				border-radius: 50%
				margin-right: 20px

				.active
					width: 14px
					height: 14px
					background-color: $black
					border-radius: 50%

			&__text
				font-size: 20px

</style>