<style>
/* Default colors */
:global(body) {
  --text-color: #222;
  --bkg-color: #fff;
  color: #222;
  background-color: #fff;
}
/* Dark theme colors */
:global(body.dark-theme) {
  --text-color: #eee;
  --bkg-color: #121212;
  color: #eee;
  background-color: #121212;
}

/* Styles for users who prefer dark mode at the OS level */
@media (prefers-color-scheme: dark) {
  /* defaults to dark theme */
  :global(body) { 
    --text-color: #eee;
    --bkg-color: #121212;
		color: #eee;
		background-color: #121212;
  }
  /* Override dark mode with light mode styles if the user decides to swap */
  :global(body.light-theme) {
    --text-color: #222;
    --bkg-color: #fff;
    color: #222;
    background-color: #fff;
  }
}
</style>

<script>
function toggleDark(){
  const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)");
  if (prefersDarkScheme.matches) {
    document.body.classList.toggle("light-theme");
  } else {
    document.body.classList.toggle("dark-theme");
  }
}
</script>

<button on:click={toggleDark}>Toggle Dark-Mode</button>
