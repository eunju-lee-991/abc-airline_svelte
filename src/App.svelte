<script>
	import { Router, Link, Route } from "svelte-routing";
	import Home from "../pages/home.svelte";
	import Reservation from "../pages/reservation.svelte";
	import Mypage from "../pages/mypage.svelte";
	import Login from "../pages/login.svelte";
</script>

<main>
	<Router >
		<nav>
			<a href="/">home</a>
			<a href="/reservation">Reservation</a>
			<a href="/mypage">Mypage</a>
		</nav>
		<Route path="/" component={Home} />
		<Route path="/reservation" component={Reservation} />
		<Route path="/mypage" component={Mypage} />
	</Router>
</main>

<style>
	main {
	  text-align: center;
	  padding: 20px;
	}
  
	nav {
	  display: flex;
	  justify-content: space-around;
	  background-color: #333;
	  padding: 10px;
	}
  
	a {
	  text-decoration: none;
	  color: white !important;
	  font-weight: bold;
	  padding: 5px 10px;
	  border-radius: 5px;
	  transition: background-color 0.3s;
	}
  
	a:hover {
	  background-color: #555;
	}
  </style>