<script>
	import Flatpickr from 'svelte-flatpickr'
    //import 'flatpickr/dist/flatpickr.css';

	//let date = new Date()
	export let startDate = null; // new Date(24*60*60*1000);
	export let endDate = null; //new Date(24*60*60*1000);
  let disabled = false;
	


var date = new Date(); // some mock date
var milliseconds = date.getTime(); 
// console.log(date, date.toLocaleString(), milliseconds)
const flatpickrOptions = {
  enableTime: true,
	//minDate: "today",
  onChange: (selectedDates, dateStr, instance) => {}
	/*
		console.log(selectedDates, dateStr, instance)
		var ms = new Date(dateStr).getTime();
		console.log('ms', ms)
	}
	*/
};
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function clickedDone() {
        if (endDate===null) {
            endDate = new Date().getTime();
        }
        if (startDate===null) {
            startDate = endDate - 24*60*60*1000
        }
		dispatch('done', {
			start: startDate,
			end: endDate,
		});
	}
	
</script>
<div>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">

<Flatpickr bind:value={startDate} placeholder="starting date and time" options={flatpickrOptions} {disabled} name="start"/>
<Flatpickr bind:value={endDate} placeholder="Ending date and time" options={flatpickrOptions} {disabled} name="end"/>
<button on:click={clickedDone} > Done emit </button> 
</div>
<!--
disbled = {disabled}
<button on:click={console.log('done',startDate, endDate)} > Done </button> 
<button on:click={() => disabled = !disabled}>
	Enable / Disable input, please
</button>
-->
