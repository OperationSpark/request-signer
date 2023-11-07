# Request Body Signer

<p align="center">
  <a href="https://github.com/actions/javascript-action/actions"><img alt="javscript-action status" src="https://github.com/actions/javascript-action/workflows/units-test/badge.svg"></a>
</p>

Use this action to sign payloads with SHA256 algorithm.
Based on https://docs.github.com/en/webhooks-and-events/webhooks/securing-your-webhooks

## Usage

```yaml
steps:
  - name: Sign payload
    id: create_signature
    uses: operationspark/request-signer@v1
    with:
      secret: ${{ secrets.SIGNING_SECRET }}
      body: ${{ env.payload }}
  - name: Echo Signature
    run: >
      echo ${{ steps.create_signature.output.signature }}
      # "sha256=acbac123bacba2342bacga..."
```

## Development

### Package for distribution

GitHub Actions will run the entry point from the action.yml. Packaging assembles the code into one file that can be checked in to Git, enabling fast and reliable execution and preventing the need to check in node_modules.

Actions are run from GitHub repos. Packaging the action will create a packaged action in the dist folder.

Run prepare

```bash
npm run prepare
```

Since the packaged index.js is run from the dist folder.

```bash
git add dist
```

### Create a release branch

Users shouldn't consume the action from master since that would be latest code and actions can break compatibility between major versions.

Checkout to the `v1` release branch

```bash
git checkout -b v1
git commit -a -m "v1 release"
```

```bash
git push origin v1
```

Note: We recommend using the `--license` option for ncc, which will create a license file for all of the production node modules used in your project.

Your action is now published! :rocket:

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)
