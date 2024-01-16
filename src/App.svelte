<script>
  import { Router, Route, Link } from 'svelte-routing';
  import Home from './routes/Home.svelte';
  import Learn from './routes/Learn.svelte';
  import Test from './routes/Test.svelte';
</script>


  
<Router>
	<style>
		:global(body, html) {
			height: 100%;
			margin: 0;
			font-family: Arial, sans-serif;
			background-color: #006d40;
			color: white;
			/* Removed flex styles to allow natural document flow */
		}

		:global(body) {
			padding-top: 70px; /* This should be equal or greater than the height of your navbar to prevent content from hiding behind it */
		}

		nav {
			display: flex;
			justify-content: center;
			gap: 20px;
			position: fixed; /* Make navbar fixed to the top */
			top: 0; /* Align to the top */
			left: 0; /* Align to the left */
			right: 0; /* Align to the right */
			background-color: #00895c; /* Same as the body background for consistency */
			z-index: 1000; /* Ensure navbar is above other content */
		} 
	  
		#nav-link {
			width: 45%;
			background-color: #00895c;
			border-radius: 15px;
			padding: 20px;
			text-align: center;
			transition: 0.3s;
			color: white; /* Ensure text color stays white on hover */
			text-decoration: none; /* Remove underline from links */
		}

		#nav-link:hover {
			box-shadow: 0 16px 32px 0 rgba(0,0,0,0.2);
			color: black; /* Ensure text color stays white on hover */
			background-color: #66db6a; /* Optional: Change background color on hover */
		}
	  
		.active {
		  background-color: #2e9d32;
		}
	</style>
	<nav>
	<Link to="dt-svelte/" id="nav-link" getProps={({ isPartiallyCurrent }) => {
		return isPartiallyCurrent ? { id: "nav-link active" } : { id: "nav-link" }
		}}>
		Strona Glowna
	</Link>
	<Link to="dt-svelte/learn" id="nav-link" getProps={({ isPartiallyCurrent }) => {
		return isPartiallyCurrent ? { id: "nav-link active" } : { id: "nav-link" }
		}}>
		Nauka
	</Link>
	<Link to="dt-svelte/test" id="nav-link" getProps={({ isPartiallyCurrent }) => {
		return isPartiallyCurrent ? { id: "nav-link active" } : { id: "nav-link" }
		}}>
		Test
	</Link>
	</nav>
	<Route path="" component={Home} />
	<Route path="/" component={Home} />
	<Route path="dt-svelte/" component={Home} />
	<Route path="dt-svelte/learn" component={Learn} />
	<Route path="dt-svelte/test" component={Test} />
</Router>
  