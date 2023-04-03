<script>
  import Result from "../lib/Result.svelte";
  import DarkToggle from "../lib/DarkToggle.svelte";
  import {tests} from "./results.json";
</script>

<DarkToggle/>

<Result {tests} />
