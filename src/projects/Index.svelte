<script>
  import DOMPurify from "dompurify";
  import marked from "marked";
  export let params = {};
  const content = fetch("public/projects/" + params.name + "/index.md");
</script>

{#await content then md}
  {#await md.text() then text}
    {#if text.length === 0}
      Not found
    {:else}
      {@html DOMPurify.sanitize(marked(text))}
    {/if}
  {/await}
{/await}
