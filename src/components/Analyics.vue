<template>
  <div class="analyics">
    <div class="analyics__switch">
      <div class="analyics__switch__tomato">
        <p class="name">TOMATO</p>
      </div>
      <div class="analyics__switch__missing">
        <p class="name">MISSING</p>
      </div>
    </div>
    <div class="analyics__focus">
      <div class="analyics__focus__head">
        <h3 class="title">FOCUS TIME</h3>
      </div>
			<div class="analyics__focus__wrap">
				<div class="analyics__focus__wrap__total">
					<p class="subtitle">TODAY</p>
					<p class="number">07<span class="tomato">/ TOMATO</span></p>
					
				</div>
				<div class="analyics__focus__wrap__total">
					<p class="subtitle">WEEK</p>
					<p class="number">60<span class="tomato">/ TOMATO</span></p>
				</div>
			</div>
    </div>
    <div class="analyics__chart">
      <div class="analyics__chart__head">
        <h3 class="title">FOCUS TIME</h3>
        <div class="picker">
          <i class="fas fa-chevron-left"></i>
          <p class="picker__date">2019/07/01 - 2019/07/07</p>
          <i class="fas fa-chevron-right"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
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
.analyics
	max-width: 525px
	width: 100%
	margin: 0 auto
	font-family: 'TaipeiSansTCBeta-Regular'

	&__switch
		display: flex
		justify-content: flex-end
		align-items: center

		&__tomato
			border: 1px solid
			border-radius: 50px 0 0 50px
			padding: 5px 15px
			background-color: $black
			color: $white

		&__missing
			border: 1px solid
			border-left: none
			border-radius: 0 50px 50px 0
			padding: 5px 15px
			position: relative
			left: -1px
		.name
			margin: 0
			font-family: 'TaipeiSansTCBeta-Light'
	
	&__focus
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
			padding: 0 24px
			&__total
				width: 50%
			.subtitle
				font-family: 'TaipeiSansTCBeta-Bold'
				font-weight: bold
				font-size: 20px
				margin: 0
				margin-top: 15px
			.number
				color: $tomatoRed
				font-size: 60px
				font-weight: bold
				margin: 0
			.tomato
				font-size: 16px
				color: $black
				font-weight: normal
				margin: 0 20px
	&__chart
		&__head
			width: calc(100% - 48px)
			height: 35px
			background-color: $black
			color: $white
			padding: 0 24px
			display: flex
			align-items: center
			justify-content: space-between
			position: relative
			margin-top: 28px
			.title
				margin: 0
			.picker
				display: flex
				justify-content: center
				align-items: center
				&__date
					font-size: 14px
					margin: 0 10px
</style>