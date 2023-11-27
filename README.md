# njump

njump is a HTTP Nostr static gateway that allows you to browse profiles, notes and relays; it is an easy way to preview a resource and then open it with your preferred client. The typical use of njump is to share a resource outside the Nostr world, where the Nostr: schema is not (yet) working.

njump has some special features to effectively share notes on platforms that offer links preview, like Twitter and Telegram.

njump currently lives under [njump.me](https://njump.me), you can reach it appending a Nostr NIP-19 entity (npub, nevent, nprofile, naddr, etc.) or a NIP-05 address after the domain, e.g. `njump.me/nevent1xxxxxx...xxx` or `njump.me/xxxx@zzzzz.com`

For more information about njump's philosophy and its use, read the presentation [on the homepage](https://njump.me).

## Supported Kinds

| kind    | description                | NIP         |
| ------- | -------------------------- | ----------- |
| `0`     | Metadata                   | [1](01.md)  |
| `1`     | Short Text Note            | [1](01.md)  |
| `6`     | Repost                     | [18](18.md) |
| `1063`  | File Metadata              | [94](94.md) |
| `1311`  | Live Chat Message          | [53](53.md) |
| `30023` | Long-form Content          | [23](23.md) |
| `30024` | Draft Long-form Content    | [23](23.md) |
| `30311` | Live Event                 | [53](53.md) |

## Running

### Running locally

The easiest way to start is to run the development server with `just` (if you have [it](https://just.systems/) installed) or with `TAILWIND_DEBUG=true go run .`. You can also check the contents of `justfile` to see other useful scripts.

For live-reload you can use [`air`](https://github.com/cosmtrek/air) and start it with `air -c .air.toml` -- this will run it without the local cache, which can be annoying if you're not specifically debugging the part of the code that loads content, so you may want to run it with `air -c .air.toml --build.cmd 'go build -o ./tmp/main .'`. These run modes will recompile the Tailwind bundle on every restart and they assume you have [the `tailwind` CLI](https://tailwindcss.com/docs/installation) installed globally.

### Running from a precompiled binary

You can grab one from the [releases](../../releases) and just run it.

### Docker

To build and run in a Docker container:

```bash
docker build -t njump .
docker run -e DOMAIN=njump.mydomain.com -p 2999:2999 njump
```
