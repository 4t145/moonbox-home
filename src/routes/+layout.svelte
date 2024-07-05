<script lang="ts">
	import '../app.css';
	import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte';

	import {
		Footer,
		FooterBrand,
		FooterCopyright,
		FooterIcon,
		FooterLink,
		FooterLinkGroup
	} from 'flowbite-svelte';

	let navbarHight: number;
</script>

<Navbar >
	<NavBrand href="/">
		<!-- <img src="/images/flowbite-svelte-icon-logo.svg" class="me-3 h-6 sm:h-9" alt="Flowbite Logo" /> -->
		<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Moonbox</span>
	</NavBrand>
	<NavHamburger></NavHamburger>
	<NavUl>
		<NavLi href="/">Home</NavLi>
		<NavLi href="/about">About</NavLi>
		<NavLi href="/contact">Contact</NavLi>
	</NavUl>
</Navbar>
<main class="flex-grow flex flex-col">
	<slot></slot>
</main>
<Footer footertype="logo" class="py-4">
	<hr class="my-2 border-gray-200 dark:border-gray-700 sm:mx-auto lg:my-4" />
	<FooterCopyright href="/" by="Flowbite™"></FooterCopyright>
</Footer>
