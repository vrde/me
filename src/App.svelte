<script>
  import { onMount } from "svelte";
  import Color from "color";
  import { ethers } from "ethers";

  import Router from "svelte-spa-router";
  import Header from "./Header.svelte";
  import Home from "./Home.svelte";
  import NotFound from "./NotFound.svelte";
  import Project from "./projects/Index.svelte";

  const routes = {
    // Exact path
    "/": Home,

    "/projects/:name": Project,

    "*": NotFound,
  };

  const provider = new ethers.providers.InfuraProvider(
    "homestead",
    "d8576e6686a94673890f22405bfc521b"
  );

  let style;
  let styleShad;
  let blockHash = "";
  let color;

  function toKebab(str) {
    return str.replace(/([A-Z])/g, (g) => `-${g[0].toLowerCase()}`);
  }

  function generateCSSVars(vars) {
    return Object.keys(vars)
      .map((name) => `--${toKebab(name)}: ${vars[name]};`)
      .join(" ");
  }

  async function updateStyle(blockNumber) {
    const block = await provider.getBlock(blockNumber);
    blockHash = block.hash;
    color = Color("#" + blockHash.substr(2, 6)).darken(0.8);
    style = generateCSSVars({
      bgColor: color.hex(),
      fgColor: color.negate().hex(),
      linkColor: color.negate().darken(0.3).hex(),
    });
  }

  function onOrientation(orientation) {
    const x = Math.max(Math.min(-orientation.gamma, 5), -5);
    const y = -Math.max(Math.min(45 - orientation.beta, 5), -5);
    styleShadow = generateCSSVars({
      shadowX: x + "px",
      shadowY: y + "px",
      // rotation: -orientation.gamma + 'deg'
    });
  }

  onMount(async () => {
    // window.addEventListener("deviceorientation", onOrientation, true);
    provider.on("block", updateStyle);
    const blockNumber = await provider.getBlockNumber();
    await updateStyle(blockNumber);
  });
  /*
   */
</script>

<main {style}>
  <div>
    <Header />
    <Router {routes} />
  </div>
</main>

<style>
  main {
    background-color: var(--bg-color, grey);
    color: var(--fg-color, #111);
    padding: 20px;
    transition: all 5s ease;
    min-height: 100%;
    line-height: 1.5;
  }

  div {
    margin: 0 auto;
    max-width: 666px;
  }

  :global(a) {
    color: var(--link-color);
    transition: all 5s ease;
  }
</style>
