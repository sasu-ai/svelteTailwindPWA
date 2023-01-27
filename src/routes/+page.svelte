<script lang="ts">
	import Keypad from '$lib/Keypad.svelte';

	let tasks = [
		{
			task: '3-3',
			solution: '0'
		},
		{
			task: '33-3',
			solution: '30'
		},
		{
			task: '3-34',
			solution: '-31'
		},
		{
			task: '323-3',
			solution: '320'
		}
	];

	let id = 0;
	let temp: Boolean;
	let input = '';

	const check = (answer: string) => {
		answer === tasks[id].solution ? (temp = true) : (temp = false);
		input = answer;
		clearInterval(myTimer);
		value = 100;
	};

	let myTimer;
	let value = 100;

	$: timeOut = () => {
		value === 0 ? clearInterval(myTimer) : null;
		value = 100;
	};
	const next = () => {
		id++;
		temp = null;
		input=''
		myTimer = setInterval(() => value--, 100);
	};
</script>

<div class="flex flex-col">
	<progress class="progress progress-primary w-4/5 mx-auto my-4" {value} max="100" />
	<div class="h-1/2 flex flex-col">
		<div class="text-6xl m-auto grow">
			{tasks[id].task} = {input}
			{#if temp}
				<span>✅</span>
			{:else if temp===false}
				<span>🚫</span>
			{/if}
		</div>
	</div>
	<Keypad on:answer={(e) => check(e.detail.text)} on:next={next} />
</div>
