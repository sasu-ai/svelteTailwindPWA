<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let input = '';
	 let answer = '';

	let state= true;
	let removeInterval: any;

	const update = async (e: any) => {
		removeRelease();
		input += e.target.dataset.symbol;
	};

	const remove = () => {
		input.length > 0 ? (input = input.slice(0, -1)) : null;
	};
	const removeHold = () => {
		removeInterval = setInterval(remove, 150);
	};
	const removeRelease = () => {
		clearInterval(removeInterval);
	};

	const send = () => {
		dispatch('answer',{text:input});
		input = '';
		state = !state;
	};

	const next = () => {
		state = !state;
		dispatch('next');
	};
</script>

<div class="absolute bottom-0 grid w-screen grow grid-cols-3 gap-2 py-4 h-1/2">
	<div class="col-span-3 input input-bordered  mx-auto w-4/5 flex items-center justify-between">
		<div class="text-2xl text-right grow">{input}</div>
		<button
			disabled={state ? false : true}
			on:click={remove}
			on:mousedown={removeHold}
			on:touchstart={removeHold}
			on:touchend={removeRelease}
			on:mouseup={removeRelease}
			class="btn btn-ghost text-2xl">⌫</button
		>
	</div>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="7"
		class="btn btn-ghost bg-red- text-2xl">7</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="8"
		class="btn btn-ghost text-2xl">8</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="9"
		class="btn btn-ghost text-2xl">9</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="4"
		class="btn btn-ghost text-2xl">4</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="5"
		class="btn btn-ghost text-2xl">5</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="6"
		class="btn btn-ghost text-2xl">6</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="1"
		class="btn btn-ghost text-2xl">1</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="2"
		class="btn btn-ghost text-2xl">2</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="3"
		class="btn btn-ghost text-2xl">3</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol=","
		class="btn btn-ghost text-2xl">,</button
	>
	<button
		disabled={state ? false : true}
		on:click={update}
		data-symbol="0"
		class="btn btn-ghost text-2xl">0</button
	>
	{#if state}
		<button on:click={send} class="btn text-2xl btn-primary">check</button>
	{:else}
		<button on:click={next} class="btn text-2xl btn-primary">next</button>
	{/if}}
</div>
