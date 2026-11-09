# Notice

## Origin and modifications

This package is an independent extraction of the Mobius Loop skill from the
oh-my-opencode project. It isn't published, reviewed, or endorsed by that
project or its maintainers.

- Source repository: [code-yeongyu/oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent)
  (formerly oh-my-opencode).
- Source revision: [`b0931bf759f5f128c6256d4789099c4171a20e1b`](https://github.com/agno01/oh-my-opencode/commit/b0931bf759f5f128c6256d4789099c4171a20e1b),
  the head of pull request #12740, on the fork branch
  `feature/mobius-loop-delivery-1794037012537`.
- Source path: `packages/omo-senpi/skills/mobius-loop/`.

Copied from that revision:

- `skills/mobius-loop/scripts/`: the engine, its type declarations, and its tests.
  Two inner callback parameters were renamed, in `assessment.mjs` and
  `status.mjs`, to satisfy this package's lint rules. Behavior is unchanged.
- `skills/mobius-loop/references/model.md`, `records.md`, and `practices.md`.
- `LICENSE.md`, from the repository root.

Modified or added by this extraction:

- `skills/mobius-loop/SKILL.md` now describes how to load the engine on any host
  that can import a local ES module. It treats `ulw-loop` delivery links and
  memory handoffs as optional.
- `skills/mobius-loop/references/omo-native.md` is new. It holds the OmO Native
  and Senpi details that the original `SKILL.md` carried inline.
- The package manifest, README, this notice, release notes, validation script,
  and CI workflows are new and belong to this standalone package.

The engine's behavior, record schema, and storage location (`.omo/mobius/<slug>/`)
are unchanged from the source revision.

## Provenance

Two pull requests to the source repository led here.

- [#1188](https://github.com/code-yeongyu/oh-my-openagent/pull/1188) proposed
  OpenCode lifecycle hooks: a `loop-detector` that flagged repeated tool calls,
  repeated errors, and read/edit ping-pong, and `definition-gates` reminders. It
  was closed without being merged.
- [#12740](https://github.com/code-yeongyu/oh-my-openagent/pull/12740) carried
  that work onto the newer architecture as a different product: an outcome
  navigation skill with a durable Node engine. It was closed without being
  merged. The maintainer declined to ship outcome navigation or a public SDK
  inside the project and suggested a standalone package instead.

This package is that outcome navigator. It doesn't detect loops, registers no
hooks, and changes nothing in the host's lifecycle. Review comments on #1188
concerned the earlier hooks and aren't an approval of this package. The
suggestion on #12740 isn't a license grant or an endorsement.

## Licensing

[LICENSE.md](LICENSE.md) reproduces the source repository's Sustainable Use
License 1.0 (SUL-1.0) in full and unchanged. It applies to this package's
program code and documentation unless a file states otherwise. That license
limits use to internal business, non-commercial, or personal purposes, and
allows distribution only free of charge for non-commercial purposes. It also
requires that modified copies carry a prominent notice of modification; the
section above is that notice.

[`skills/mobius-loop/references/model.md`](skills/mobius-loop/references/model.md)
adapts explanatory material from Open Practice Library and the Mobius Loop
model under Creative Commons Attribution-ShareAlike 4.0. Its attribution and
license statement are kept as written in that file.

No other license has been granted or assumed. Relicensing the extracted files
would need permission from the licensor of the source repository, and none has
been sought or given.
