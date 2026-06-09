# granzotto.net

Alberto Granzotto's personal site. Static, built with [Astro](https://astro.build).

## Develop

```sh
bun install
bun run dev      # http://localhost:4010
```

## Build

```sh
bun run build    # static output in dist/
bun run preview  # preview the built site
```

## Notes

- The landing (`src/pages/index.astro`) leads with a dithered portrait hero
  (`src/components/DitherHero.astro`) — Bayer ordered dithering on a `<canvas>`,
  scroll-driven from coarse to fine.
- The page palette is derived from the latest Ethereum block hash
  (`src/scripts/blockColor.js`) — a keyless JSON-RPC call, no wallet libraries.
- The `/ai` workshop page is hand-authored HTML served verbatim from `public/ai/`.
- `public/CNAME` carries the custom domain into the build output.
