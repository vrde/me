<script>
	import { onMount } from 'svelte';
  import Color from "color";
  import ethers from "ethers";
  const provider = ethers.getDefaultProvider();
  let style;
  let styleLinks;

  async function updateStyle(blockNumber) {
    const block = await provider.getBlock(blockNumber);
    const blockHash = block.hash;
    const color = Color("#" + blockHash.substr(2, 6)).darken(0.6);
    style = `color: ${color.hex()}; background-color: ${color.negate().hex()}`;
    styleLinks = `color: ${color.lighten(0.5).hex()}`;
  }

  onMount(async () => {
    provider.on("block", updateStyle);
    const blockNumber = await provider.getBlockNumber();
    await updateStyle(blockNumber);
  });
/*
  */

</script>

<style>
  div {
    background-color: grey;
    color: #111;
    transition: background-color 5s ease;
    padding: 20px 80px;
  }
</style>

<div style={style}>
<h1>Alberto Granzotto</h1>
<p>
I'm a freelance software engineer interested in decentralization,
protocols, networking (not the one with business cards), hardware, and
open source.
</p>

<h2>Currently working on</h2>
<ul>
  <li>
    Renovating the main
    <a href="https://github.com/tracking-exposed/web-extension"
       >web extension</a
     >
     for <a href="https://tracking.exposed/">Tracking Exposed</a>, an
     initiative to increase transparency behind personalization algorithms.
  </li>

  <li>
    Hardware and software development for Package Point, a locker system to
    speed up delivery and pick-up of parcels.
  </li>

  <li>
    Protocol design and smart contract development for
    <a href="https://github.com/urbi-mobility/contracts/">Ditto</a>, an
    identity protocol for mobility providers developed under
    <a href="https://urbi.co">Urbi</a>.
  </li>

  <li>
    <a href="https://leapdao.org/">LeapDAO</a> as an occasional contributor.
  </li>

  <li>
    Doing weird^H^H^H^H^Hcreative projects with
    <a href="https://github.com/social-dist0rtion-protocol"
       >Social Dist0rtion Protocol</a
     >, a collective from the year 2055.
  </li>
</ul>
<h2>Recent projects</h2>
<ul>
  <li>
    <a href="https://gitcoin.co/grants/127/planet-a">Planet A</a> is a
    <em>simulation game</em> to raise awareness on climate change, developed
    by Social Dist0rtion Protocol and LeapDAO.
  </li>
  <li>
    <a href="https://github.com/vrde/ethnode">ethnode</a> is a zero
    configuration tool to run a local Ethereum node. It supports both Parity
    and Geth.
  </li>
</ul>

<h2>Previous projects</h2>
<ul>
  <li>
    Core developer for <a href="https://www.bigchaindb.com">BigchainDB</a>.
  </li>
  <li>Core developer for <a href="https://ascribe.io">ascribe</a>.</li>
  <li>
    Founder of isoverse, a tool for creatives to manage their portfolio
    using dropbox.
  </li>
  <li>
    Founder of
    <a href="https://medium.com/@vrde/epilogue-18698396094">Urlist</a>, a
    bookmarking service.
  </li>
  <li>Developer for embedded devices for street lighting.</li>
</ul>

<h2>Playing with</h2>
<ul>
  <li>
    <a href="https://svelte.dev">Svelte</a> is pretty fun. This website is
    built with svelte—yep that's overkill—but.
  </li>
  <li><a href="https://www.albertogranzotto.com">Photography</a>.</li>
</ul>

<h2>Contact</h2>
<ul>
  <li><a href="https://twitter.com/vrde">vrde on Twitter</a></li>
  <li><a href="https://github.com/vrde">vrde on GitHub</a></li>
  <li><a href="mailto:agranzot@mailbox.org">email</a></li>
</ul>

<h2>About this site</h2>
<p>The background changes color every time a new block in the Ethereum network is mined.</p>
</div>
