<script>
  import Result from "../lib/Result.svelte";
  import DarkToggle from "../lib/DarkToggle.svelte";
  import resultData from "./results.json";
</script>

<DarkToggle/>

<Result {resultData} />
