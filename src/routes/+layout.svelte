<script>
	import { afterNavigate, beforeNavigate, onNavigate, goto } from '$app/navigation';

	let beforeNav = '';
	let onNav = '';

	beforeNavigate(async (navigation) => {
		console.log('beforeNavigate');
		beforeNav = 'pending';
		navigation.complete.catch(() => {}).finally(() => {
			console.log('beforeNavigate complete')
			beforeNav = 'complete'
		})
	})

	onNavigate(async (navigation) => {
		console.log('onNavigate');
		onNav = 'pending';
		navigation.complete.catch(() => {}).finally(() => {
			console.log('onNavigate complete')
			onNav = 'complete'
		})
	});

	afterNavigate(() => {
		console.log('afterNavigate')
	})
</script>

<p>home and about work fine, but when navigating to /thingy or /stuff the beforeNavigate navigation.complete promise never rejects or resolves.</p>

<a href="/">home link</a>
<button type="button" on:click={() => goto('/')}>home goto</button>
<br>
<a href="/about">about link</a>
<button type="button" on:click={() => goto('/about')}>about goto</button>
<br>
<a href="/thingy">thingy link</a>
<button type="button" on:click={() => goto('/thingy')}>thingy goto</button>
<br>
<a href="/stuff">stuff link</a>
<button type="button" on:click={() => goto('/stuff')}>stuff goto</button>
<br>

<br>
<div>beforeNavigate: {beforeNav}</div>
<div>onNavigate: {onNav}</div>

<br><br>
<slot/>
