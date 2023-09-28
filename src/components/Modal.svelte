<script>
  import Dialog from "@smui/button";

  export let open = false;
</script>

<div>
  <Dialog
    bind:open
    aria-labelledby="simple-title"
    aria-describedby="simple-content"
  >
    <h1>This is modal.</h1>
  </Dialog>
</div>
