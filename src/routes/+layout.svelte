<script>
	import { onMount } from 'svelte';
	import { base } from '$app/paths';
	import { darkModeStore } from '$lib/stores/darkModeStore.js';

	onMount(async () => {
		darkModeStore.init();
	});

	$: darkMode = $darkModeStore;
	let navBar = '';

	// darkMode handler
	$: {
		if (darkMode == true) {
			navBar = 'bg-dark';
			darkModeStore.set(JSON.stringify(true));
		} else if (darkMode == false) {
			navBar = 'bg-light';
			darkModeStore.set(JSON.stringify(false));
		}
	}
</script>

<svelte:head>
	<meta name="DARK_MODE" content={darkMode} />
</svelte:head>

<nav class="navbar navbar-expand-lg fixed-top {navBar} border-bottom">
	<div class="container">
		<a href="{base}/" class="navbar-brand"> <span editable="inline">Sveltekit template</span> </a>

		<button
			class="navbar-toggler"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#myNavbar1"
			aria-controls="myNavbar1"
			aria-expanded="false"
			aria-label="Toggle navigation"
		>
			<span class="navbar-toggler-icon" />
		</button>
		<div class="collapse navbar-collapse" id="myNavbar1">
			<div lc-helper="shortcode" class="live-shortcode me-auto">
				<ul id="menu-menu-1" class="navbar-nav me-auto mb-2 mb-md-0 navbar-nav">
					<li
						class="menu-item menu-item-type-custom menu-item-object-custom nav-item nav-item-32739"
					>
						<a href="{base}/" class="nav-link">Home</a>
					</li>
					<li
						class="menu-item menu-item-type-custom menu-item-object-custom menu-item-home nav-item nav-item-32738"
					>
						<a href="{base}/about/" class="nav-link">About</a>
					</li>
				</ul>
			</div>
			<form>
				<div class="form-check form-switch">
					<input
						class="form-check-input"
						id="darkMode"
						type="checkbox"
						name="darkMode"
						bind:checked={darkMode}
					/>
					<label class="form-check-label" for="darkMode">Dark mode</label>
				</div>
			</form>
		</div>
	</div>
</nav>

<div class="p-5" />

<main>
	<slot />
</main>

<section class="border-top p-3 mt-5">
	<div class="container py-6 text-center">
		<div class="lc-block">
			<div editable="rich">
				<p class="text-muted">© 2023 realskyquest</p>
			</div>
		</div>
	</div>
</section>
