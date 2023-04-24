<script lang="ts">
export let path: string;

// TODO these two should be put in stores
// instead of being global variables controlled
// by the parent component
export let jupyter_server_url: string;
export let jupyter_server_token: string;

$: hyperlink =  jupyter_server_url +  "tree/" + path + "?token=" + jupyter_server_token;
</script>

<p>
Path: {path}
</p>

<a rel="noreferrer" target="_blank" href={hyperlink} >
{hyperlink}
</a>

^ For this to work, start jupyter in the folder containing all the submissions (submission_nnnnnnn). (jupyter notebook .). Adjust text inputs in top left if necessary.
