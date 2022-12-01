<script lang="ts">
	import MapView from "@arcgis/core/views/MapView";
	import "@arcgis/core/assets/esri/themes/light/main.css";

	let centerText: string;

	const defaultMapCenter = [-122.2708, 37.8044];

	const createMap = (domNode: HTMLDivElement) => {
		const view = new MapView({
			container: domNode,
			map: {
				basemap: "streets-vector",
			},
			zoom: 12,
			center: defaultMapCenter,
		});

		view.watch("center", (center: MapView["center"]) => {
			const { latitude, longitude } = center;
			centerText = `Map centered at lon: ${longitude.toFixed(
				4
			)}, lat: ${latitude.toFixed(4)}.`;
		});
	};
</script>

<main>
	<div class="view" use:createMap />
	<p>{centerText}</p>
</main>

<style>
	.view {
		height: 400px;
		width: 800px;
	}
</style>
