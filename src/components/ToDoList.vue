<template>
  <div class="todo-list">
		<div class="todo-list__wrap">
			<input
				v-model="newTodo"
				placeholder="ADD NEW MISSION…"
				class="todo-list__wrap__input">
			<div
				class="todo-list__wrap__button"
				@click="addTodo">
				<i class="fas fa-plus"></i>
			</div>
		</div>
		<div class="todo-list__todo">
			<div 
				class="title__wrap"
				@click="openTodo">
				<h3 class="title__wrap__text">TO-DO</h3>
				<div
					:class="{ open: isTodoOpen }"
					class="title__wrap__arrow"></div>
			</div>
			<div
				v-for="item in toDos"
				v-if="isTodoOpen"
				:key="item"
				class="items__wrap">
				<div
					class="items__wrap__check"
					@click="doneTodo(item)">
					<i class="far fa-circle"></i>
				</div>
				<p
					class="items__wrap__text"
					v-text="item"></p>
				<div class="items__wrap__play">
					<i
						v-if="nowPlaying === item" 
						class="far fa-pause-circle"></i>
					<i
						v-else
						class="far fa-play-circle"
						@click="setNowPlaying(item)"></i>
				</div>
			</div>
		</div>
		<div class="todo-list__done">
			<div
				class="title__wrap"
				@click="openDone">
				<h3 class="title__wrap__text">DONE</h3>
				<div
					:class="{ open: isDoneOpen }"
					class="title__wrap__arrow"></div>
			</div>
			<div
				v-for="item in dones"
				v-if="isDoneOpen"
				:key="item"
				class="items__wrap">
				<div
					class="items__wrap__check"
					@click="cancelDone(item)">
					<i class="far fa-check-circle"></i>
				</div>
				<p
					class="items__wrap__text"
					v-text="item"></p>
			</div>
		</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      toDos: [
				'first thing',
				'second thing',
				'third thing'
			],
			dones: [
				'done 1'
			],
			isTodoOpen: true,
			isDoneOpen: false,
			newTodo: '',
			nowPlaying: 'first thing'
    }
	},
	mounted() {
		this.$emit('set-now-playing', this.nowPlaying)
	},
	methods:{
		openTodo() {
			this.isTodoOpen = !this.isTodoOpen
		},
		openDone() {
			this.isDoneOpen = !this.isDoneOpen
		},
		addTodo() {
			this.toDos.push(this.newTodo)
			this.newTodo = ''
		},
		doneTodo(todo) {
			const todoIndex = this.toDos.indexOf(todo)
			this.toDos.splice(todoIndex, 1)
			this.dones.push(todo)
			if(this.nowPlaying === todo)
				this.nowPlaying = this.toDos[0]
		},
		cancelDone(done) {
			const doneIndex = this.dones.indexOf(done)
			this.dones.splice(doneIndex, 1)
			this.toDos.push(done)
		},
		setNowPlaying(item) {
			this.nowPlaying = item
			this.$emit('set-now-playing', this.nowPlaying)
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

.todo-list
	max-width: 525px
	width: 100%
	margin: 0 auto

	&__wrap
		position: relative

		&__input
			width: calc(100% - 58px)
			height: 70px
			font-size: 18px
			font-family: TaipeiSansTCBeta-Bold
			font-weight: bold
			padding: 0 28px
			border: 1px solid $darkGray

			&::placeholder
				color: $tomatoRed

		&__button
			color: $tomatoRed
			position: absolute
			font-size: 18px
			top: 50%
			right: 28px
			transform: translateY(-50%)
			cursor: pointer

	&__todo
		
	&__done
		.items__wrap__text
			text-decoration: line-through
	.title__wrap
		width: calc(100% - 48px)
		height: 35px
		background-color: $black
		color: $white
		padding: 0 24px
		display: flex
		align-items: center
		position: relative
		margin-top: 28px
		cursor: pointer

		&__text
			margin: 0

		&__arrow
			position: absolute
			right: 24px
			width: 0
			height: 0
			border-style: solid
			border-width: 0 6.5px 8px 6.5px
			border-color: transparent transparent $white transparent
			transition: all 0.3s ease

		.open
			transform: rotate(180deg)

	.items__wrap
		display: flex
		align-items: center
		justify-content: space-between
		padding: 0 24px
		height: 55px
		border-bottom: 1px solid $darkGray
		&__check
			cursor: pointer
			&:hover
				color: $tomatoRed
		&__text
			margin: 0
			width: 80%

		&__play
			cursor: pointer
			&:hover
				color: $tomatoRed

		i
			font-size: 20px
</style>