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
	let temp = '';

	const check = (answer: string) => {
		answer === tasks[id].solution ? (temp = 'correct') : (temp = 'falsch');
	};

	const next = () => {
		id++;
		temp = '';
	};
</script>

<div class="">
	<div>{tasks[id].task}</div>
	<div>{temp}</div>
	<Keypad on:answer={(e) => check(e.detail.text)} on:next={next} />
</div>
