<script>
	import '../app.css';
	import Drawer, { AppContent, Content } from '@smui/drawer';
	import List, { Item, Text } from '@smui/list';
	import { page } from '$app/stores';

	let clicked = 'nothing yet';
	import TopAppBar, { Row, Section, Title } from '@smui/top-app-bar';
	import IconButton from '@smui/icon-button';
	let prominent = false;
	let dense = false;
	let secondaryColor = false;
	let open = true;
	$: path = $page.url.pathname;
</script>

<div class="flexy">
	<div class="top-app-bar-container">
		<TopAppBar
			variant="static"
			{prominent}
			{dense}
			color={secondaryColor ? 'secondary' : 'primary'}
		>
			<Row>
				<Section>
					<IconButton on:click={() => (open = !open)} class="material-icons">menu</IconButton>
					<Title>Static</Title>
				</Section>
				<Section align="end" toolbar>
					<!-- <IconButton class="material-icons" aria-label="Download">file_download</IconButton>
					<IconButton class="material-icons" aria-label="Print this page">print</IconButton>
					<IconButton class="material-icons" aria-label="Bookmark this page">bookmark</IconButton> -->
					<!-- <button class="logoutBtn">Log out</button> -->
					<i class="iconLogout fa-solid fa-arrow-right-from-bracket" />
				</Section>
			</Row>
		</TopAppBar>
	</div>
</div>

<div class="drawer-container">
	<Drawer variant="dismissible" bind:open>
		<Content>
			<List>
				<Item href="/grayKittens" activated={path.startsWith('/grayKittens')}>
					<Text>Gray Kittens</Text>
				</Item>
				<Item href="/aSpaceRocket" activated={path.startsWith('/aSpaceRocket')}>
					<Text>A Space Rocket</Text>
				</Item>
				<Item href="/100PoundsOfGravel" activated={path.startsWith('/100PoundsOfGravel')}>
					<Text>100 Pounds of Gravel</Text>
				</Item>
				<Item href="/allOfTheShrip" activated={path.startsWith('/allOfTheShrip')}>
					<Text>All of the Shrimp</Text>
				</Item>
				<Item href="/aPlanetWithAMall" activated={path.startsWith('/aPlanetWithAMall')}>
					<Text>A Planet with a Mall</Text>
				</Item>
			</List>
		</Content>
	</Drawer>

	<AppContent class="app-content">
		<main class="main-content">
			<!-- App content.
			<br />
			<pre class="status">Clicked: {clicked}</pre> -->
			<slot />
		</main>
	</AppContent>
</div>

<style>
	:global(.drawer-container > .mdc-drawer) {
		height: calc(100vh - 64px);
	}
	/* These classes are only needed because the
	  drawer is in a container on the page. */
	.drawer-container {
		/* position: relative; */
		display: flex;
		/* height: 350px;
		max-width: 600px; */
		/* border: 1px solid var(--mdc-theme-text-hint-on-background, rgba(0, 0, 0, 0.1)); */
		overflow: hidden;
		z-index: 0;
	}

	:global(.app-content) {
		flex: auto;
		overflow: auto;
		position: relative;
		flex-grow: 1;
	}

	.main-content {
		overflow: auto;
		padding: 16px;
		height: 100%;
		box-sizing: border-box;
	}
	.iconLogout {
		cursor: pointer;
		font-size: 1.5rem;
		margin-right: 1.5rem;
		transition: all 0.15s;
	}
	.iconLogout:hover {
		color: blueviolet;
	}
	.logoutBtn {
		border: 1px solid white;
		padding: 10px;
		background-color: blue;
		border-radius: 5px;
		transition: all 0.5s;
		margin-right: 1.2rem;
	}
	.logoutBtn:hover {
		background-color: yellow;
	}
	.top-app-bar-container {
		/* max-width: 480px; */
		width: 100%;
		/* height: 320px; */
		/* border: 1px solid var(--mdc-theme-text-hint-on-background, rgba(0, 0, 0, 0.1)); */
		/* margin: 0 18px 18px 0; */
		background-color: var(--mdc-theme-background, #fff);

		overflow: auto;
		display: inline-block;
	}

	@media (max-width: 480px) {
		.top-app-bar-container {
			margin-right: 0;
		}
	}

	.flexy {
		display: flex;
		flex-wrap: wrap;
	}

	.flexor {
		display: inline-flex;
		flex-direction: column;
	}

	.flexor-content {
		flex-basis: 0;
		height: 0;
		flex-grow: 1;
		overflow: auto;
	}
</style>
