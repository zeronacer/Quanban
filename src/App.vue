<template>
	<div id="app">

		<!-- START navbar -->
		<b-navbar toggleable="lg" type="dark" variant="dark">
			<b-navbar-brand href="#">Quanban</b-navbar-brand>

			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<!-- Right aligned nav items -->
				<b-navbar-nav class="ml-auto">
					<b-nav-form>
						<b-form-input id="inputNewFlowline" v-model="newFlowline" required
							placeholder="Flusslinie hinzufügen..." @keyup.enter="add" class="mb-2 mr-sm-2 mb-sm-0">
						</b-form-input>
						<b-button @click="add" variant="success" class="ml-1">+</b-button>
					</b-nav-form>
				</b-navbar-nav>
			</b-collapse>
		</b-navbar>
		<!-- END navbar -->

		<!-- START content -->
		<div class="d-flex m-5 justify-content-center">
			<div class="filler-content-container" v-show="arrFlowlines.length <= 0">
				<h2>Oh nein!</h2>
				<p>Du hast gar keine Flusslinien. Oben rechts kannst du deine Erste erstellen!</p>
			</div>
			<draggable handle=".handle" class="d-sm-flex" :list="arrFlowlines" group="flowlines">
				<Flowline v-for="flowline in arrFlowlines" :key="flowline.name" :title="flowline.name"
					v-on:delete-flowline="deleteFlowline"></Flowline>
			</draggable>
		</div>
		<!-- END content -->

		<!-- START footer -->
		<footer class="footer py-3 bg-light">
			<span class="text-muted">von zeronacer</span>
			<span>|</span>
			<a href="https://github.com/zeronacer/Quanban">Github</a>
			<span>|</span>
			<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
				<input type="hidden" name="cmd" value="_s-xclick" />
				<input type="hidden" name="hosted_button_id" value="ZRJU3QEJ7BRHN" />
				<input type="image" src="https://www.paypalobjects.com/de_DE/DE/i/btn/btn_donate_SM.gif" border="0"
					name="submit" title="PayPal - The safer, easier way to pay online!"
					alt="Spenden mit dem PayPal-Button" />
				<img alt="" border="0" src="https://www.paypal.com/de_DE/i/scr/pixel.gif" width="1" height="1" />
			</form>
		</footer>
		<!-- END footer -->

	</div>
</template>

<script>
import draggable from "vuedraggable";
import Flowline from "./components/Flowline.vue"
export default {
	name: "kanban-board",
	components: {
		Flowline,
		draggable
	},
	metaInfo: {
		meta: [{
			name: "viewport",
			content: "width=device-width, initial-scale=1"
		}]
	},
	data() {
		return {
			// for new tasks
			newFlowline: "",
			// 4 arrays to keep track of our 4 statuses
			arrFlowlines: []
		};
	},
	methods: {
		//add new tasks method
		add: function () {
			if (this.newFlowline) {
				this.arrFlowlines.push({
					name: this.newFlowline
				});
				this.newFlowline = "";
			}
		},
		deleteFlowline: function (flowlineTitle) {
			this.arrFlowlines = this.arrFlowlines.filter(function (obj) {
				return obj.name !== flowlineTitle;
			})
		}
	}
};
</script>

<style>
.filler-content-container {
	text-align: center;
	width: 100%;
}

.footer {
	display: flex;
	justify-content: center;
	position: fixed;
	bottom: 0;
	left: 0;
	width: 100%;
	text-align: center;
}

.footer form {
	border-left: 5px solid transparent;
	border-right: 5px solid transparent;
}

.footer span {
	border-left: 5px solid transparent;
	border-right: 5px solid transparent;
}

.footer a {
	border-left: 5px solid transparent;
	border-right: 5px solid transparent;
}

.form-control {
	width: auto !important;
}
</style>