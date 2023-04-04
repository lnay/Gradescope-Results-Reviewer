<script>
  import Result from "../lib/Result.svelte";
  import DarkToggle from "../lib/DarkToggle.svelte";
  import {tests} from "./results.json";

  $: test_filter = (test) => test.name.match(pattern);
  let pattern = ".*";
</script>

<DarkToggle/>
<br/>

<button on:click={ ()=>{pattern = ".*";} }>all</button>
<button on:click={ ()=>{pattern = "^1";} }>Task 1</button>
<button on:click={ ()=>{pattern = "^2";} }>Task 2</button>
<button on:click={ ()=>{pattern = "^3";} }>Task 3</button>
<br/>

<label>
search: <input bind:value={pattern}/>
</label>
<br/>

<Result {tests} {test_filter} />
