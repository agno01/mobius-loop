# Releasing

Nothing is published. The package is `private`, has no public repository, and
no registry name has been claimed. Publishing needs separate decisions about
ownership, the package name, the license, and the publishing identity.

## Build a release candidate

The **Prepare release candidate** workflow
(`.github/workflows/release-candidate.yml`) runs only by manual dispatch. It
installs with the frozen lockfile, runs `bun run check`, packs the tarball, and
uploads it as the `mobius-loop-release-candidate` artifact. It doesn't publish,
tag, or push anything.

To build the same artifact locally:

```sh
bun install --frozen-lockfile
bun run check
mkdir artifacts && bun pm pack --destination artifacts
```

## Verify the candidate

Run these against the packed tarball, unpacked outside the source checkout,
never against the working tree.

1. The file list holds only `package.json`, `README.md`, `LICENSE.md`,
   `NOTICE.md`, `SKILL.md`, the references, and the runtime `.mjs` and `.d.mts`
   files. No tests, workspace links, or developer paths.
2. `bun script/validate.ts <unpacked-dir>` passes.
3. The unpacked engine imports under plain Node at the minimum supported
   version, finds its own files by relative path, and creates and resumes an
   initiative across two processes.
4. In an isolated OmO Native home, `omo install <unpacked-dir>` succeeds, the
   skill is discovered from that directory, and `/skill:mobius-loop` records and
   resumes a real initiative after a restart. Exercise a `ulw-loop` link and the
   learning handoff, then confirm `omo remove` leaves `.omo/mobius/` intact.
5. With a same-name copy also present, the collision warning appears, the
   object entry with `"skills": []` disables this package, and the selected
   path is the expected one.
6. Every platform and runtime the README claims has run step 3. Engine and
   artifact checks cover macOS ARM64 and Windows Server 2025 x64 with Node
   24.22.2. The host journey in step 4 also covers both platforms with OmO
   Native 5.1.65. Resource-loader checks use the matching Senpi engine:
   2026.11.5-1 on macOS and 2026.11.6-3 on Windows. Retain startup and shutdown
   warnings with the QA results; these runs don't certify the host's
   background services or autonomous model behavior.

## Version

Bump `version` in `package.json`. If the tarball name changes, update the paths
in the README. Records keep `schemaVersion: 1`. Changing the storage path or
the `deliveryRef` union needs its own tested migration and isn't part of a
routine release.

## Before the first publication

These steps wait for the decisions above.

- Settle the package name and owner, then add `repository` and the agreed
  license metadata.
- Remove `private` only in the change that publishes.
- Add a publish job that ships the verified candidate artifact rather than
  rebuilding it, using a credential owned by the package.
- Document a pinned install, such as `omo install npm:<name>@<version>` or a
  git source at a tag. Pinned sources don't move on a general update, so
  upgrading means installing the new pinned version on purpose. Check those
  exact commands against the installed host before documenting them.
