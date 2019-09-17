<template>
	<div ref="navbar_primary" :class="{'auto-margin-top': enable_fixed_nav}">
		<div :class="{'fixed-nav': enable_fixed_nav}" class="component_navbar_primary">
			<slot name="nav-content"></slot>
		</div> 
	</div>
</template>

<script>
export default {
	data () {
		return {
			enable_fixed_nav: false,
			menu_height: 0
		}
	},
	created () {
		/*
			TODO: Agregamos listener antes de quitar el component
		*/
		window.addEventListener('scroll', this.handleScroll);
	},
	mounted() {
		/*
			TODO: Asignamos el tamaño real del menu a la variable "menu_height"
		*/
		this.menu_height = this.$refs.navbar_primary.offsetHeight
	},
	beforeDestroy() {
		/*
			TODO: Destruimos el listener antes de quitar el component
		*/
		window.removeEventListener('scroll', this.handleScroll);
  	},
	methods: {
		handleScroll () {
			/*
				TODO: Metodo para mostrar el menu cuando se hace scroll.
			*/
			let	vm = this
			vm.enable_fixed_nav = window.scrollY > vm.menu_height
		}
	}
}
</script>

<style lang="scss">
.auto-margin-top {
	margin-top: 48px;
}

.component_navbar_primary{
	position: relative;
	&.fixed-nav {
		position: fixed;
		width: 100%;
		top: 0;
		animation-duration: 1s;
		animation-name: slidein;
		animation-timing-function: cubic-bezier(0.68, -0.55, 0.52, 1);
		box-sizing: border-box;
	}
}

@keyframes slidein {
	from {
		top: -48px;
	}
	to {
		top: 0;
	}
}
</style>