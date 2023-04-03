<script>
  import Result from "../lib/Result.svelte";
  import DarkToggle from "../lib/DarkToggle.svelte";
  import {tests} from "./results.json";

  let test_filter = (_test) => true;


</script>

<DarkToggle/>
<br/>
<button on:click={
	()=>{test_filter = (_test) => true;}
}>all</button>
<button on:click={
	()=>{test_filter = (test) => test.name.match(/^1/);}
}>Task 1</button>
<button on:click={
	()=>{test_filter = (test) => test.name.match(/^2/);}
}>Task 2</button>
<button on:click={
	()=>{test_filter = (test) => test.name.match(/^3/);}
}>Task 3</button>

<Result {tests} {test_filter} />
