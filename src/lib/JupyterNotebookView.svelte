<script>
export let path="aoeu";
export let jupyter_server_url;
export let jupyter_server_token;

$: link =  jupyter_server_url +  "tree/" + path + "?token=" + jupyter_server_token;
</script>

<p>
Path: {path}
</p>

<a rel="noreferrer" target="_blank" href={link} >
{link}
</a>

^ For this to work, start jupyter in the folder containing all the submissions (submission_nnnnnnn). (jupyter notebook .). Adjust text inputs in top left if necessary.
