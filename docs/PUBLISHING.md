# Publication preparation

This public repository is distributed through Git. Release `v0.1.0` was accepted into the Paseo registry on 2026-11-06 as `ivolnistov/drawio`. The repository was transferred to `GaijinEntertainment` on 2026-11-19; migration of the catalog identity to `gaijinentertainment/drawio` requires registry review. No npm publication is required for this route; `private: true` in `package.json` deliberately prevents accidental npm publication.

## Release checks

- Run the typecheck and tests with a compatible Node version.
- Check `npm pack --dry-run --ignore-scripts` includes the runtime entries, imported modules, bundled viewer and shape index, licenses, shrinkwrap, overview, examples and both manifest media files.
- Confirm screenshots show the current interface with sample data and no private details.
- Check the final public tree and author metadata before changing visibility. The owner-authorized history squash and removal of six checkpoint branches are complete; a private recovery bundle preserves the original history. The current tree still includes internal planning and acceptance reports.
- Install the selected Git revision on an isolated test daemon and exercise the file panel, inline rendering and agent tools.
- Verify routing uses the library bundled in the pinned `@drawio/mcp` package without network requests or a previously downloaded cache. The adapter points the package's exported routing-source object at that local file; dependency upgrades must recheck that internal interface and the vendored path.
- Resolve or document the availability of corresponding source for the optional ELK bundle. See `NOTICE.md`; the bundle is downloaded rather than shipped in this repository.
- Obtain owner approval of the final repository text, public visibility change and submission text before publishing them.

## GitHub releases

Pushing a tag `vX.Y.Z` (or `vX.Y.Z-<prerelease>`) runs `.github/workflows/release.yml`:

1. The tag must equal `v` plus the `version` in `package.json`, and `npm-shrinkwrap.json` must carry the same version at its top level and in `packages[""]`. Bump all three before tagging.
2. The full checks (`checks.yml`: typecheck and all tests with the verified ELK bundle) run once for the tag; a failure stops the release.
3. `npm pack --ignore-scripts` builds `paseo-plugin-drawio-X.Y.Z.tgz`, and `SHA256SUMS` records its checksum.
4. `gh release create --verify-tag` publishes a GitHub Release with both files and fixed notes containing the tag install command. A version with a prerelease suffix is marked as a prerelease. Nothing is published to npm.

The archive holds the plugin source, assets, licenses and the lock, without dependencies. Paseo installs from the Git tag (`paseo plugin add git:GaijinEntertainment/paseo-plugin-drawio --ref vX.Y.Z`), not from the archive. Pushing a tag is a publication step and needs owner approval like the others above.

`npm-shrinkwrap.json` is the committed dependency lock for this repository; `npm ci` consumes it. There is no separate `package-lock.json`.

The screenshots and metadata are release materials, not a statement that registry review has completed. Preserve any remaining validation gaps in the release record.

## GitHub destination

Repository: <https://github.com/GaijinEntertainment/paseo-plugin-drawio>

Repository description:

> View draw.io diagrams in Paseo file tabs and agent replies, and give agents the official draw.io tools

The repository remains public after the transfer. Registry reviewers pin the exact reviewed commit.

## Registry submissions

Destination: <https://github.com/getpaseo/plugins/issues/new?template=submit-plugin.yml>

Title: `draw.io`

Use the submission form so the issue receives the required `submission` label. It has only Source and Categories fields; [SUBMISSION.md](SUBMISSION.md) contains those values. Source defaults to `main`; supply the final commit URL instead if a specific release should be reviewed. The manifest declares both screenshot paths, so the reviewer can resolve them from the selected revision. No additional comment is proposed.

After submission, record the issue and generated review PR. Git updates require a new submission or an explicit revision request; they do not automatically follow `main`.

## References

- [Paseo publishing guide](https://paseo.sh/docs/plugins/publishing)
- [Registry review policy](https://github.com/getpaseo/plugins/blob/main/REVIEW.md)
- [Submission form](https://github.com/getpaseo/plugins/issues/new?template=submit-plugin.yml)

Transfer and registry behavior checked on 2026-11-19. Registry review is separate from local tests and installation checks.

## Ownership transfer

The manifest ID remains `drawio`. GitHub redirects the former repository URL to the corporate repository; do not reuse the old repository location. Tags and releases retain their existing commits.

Keep the existing `ivolnistov/drawio` registry record available during migration so installed copies can still resolve their pinned artifact. The proposed corporate catalog ID is `gaijinentertainment/drawio`. Existing registry installations track their original ID and do not automatically switch to another ID. If a registry pin changes its Git remote, Paseo requires reinstallation to approve the new source. Coordinate retirement of the legacy record with the registry maintainers.

The personal `PASEO_REGISTRY_TOKEN` Actions secret was removed before the transfer. Automatic registry submissions are not enabled on the published branch. A separately authorized corporate credential and the pending submission workflow must be configured before enabling that automation. GitHub release creation still uses the repository's default `GITHUB_TOKEN`.
