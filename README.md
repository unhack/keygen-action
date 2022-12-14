# Release to Keygen.sh (Github Action)

This Github action creates (and, if needed, publishes) a release for any artifact/file from your repository.

## Usage

```yaml
- name: Release to Keygen
  uses: unhack/keygen-action@main # TODO: update action ref
  with:
    # Required: Keygen Account ID or slug
    account-id: 'your-keygen-account-id-or-slug'

    # Required: A Product or User Token (ref. https://keygen.sh/docs/api/authentication/#token-authentication)
    token: 'your-token'

    # Required: Product ID
    product-id: 'your-product-id'

    # Required (boolean): true to publish the created release; false to keep it in the DRAFT state.
    release-publish: true

    # Optional
    release-name: 'Product v1-alpha.1'
    # Required: must be a valid semver value, without the `v` prefix
    release-version: '1.0.0-alpha.1'
    # Required
    release-channel: 'alpha'
    # Optional
    release-tag: 'latest'

    # Required: A json list of artifact/file definitions
    #   - filepath:  Required
    #   - platform:  Optional
    #   - arch:      Optional
    # N.B. Notice the syntax for the example field below is a Multiline string (do not forget the preceding `|` char). Ordinary single-line json strings are also accepted.
    # N.B. The actual files need to be made available in the Github Runner runtime through any adequate preceeding workflow step
    # e.g. using the 'actions/checkout@v3' Github action for checking-out Github repository files.
    artifacts-json: |
      [
        {
          "filepath": "./file1.ext",
          "platform": "darwin",
          "arch": "amd64"
        },
        {
          "filepath": "./file2.ext",
          "platform": "darwin",
          "arch": "amd64"
        }
      ]
```

## :construction: TODO (WIP):

- [x] Feature: :white_check_mark: Releases for **single artifacts/files**
- [x] Feature: Add support for releases with **multiple associated artifacts/files**
- [ ] Feature: Better error logs
  - Currently, `core.setFailed(Error)` usages only show the `Error.message` value, which does not provide enough info in Action console logs, yet.
  - Our custom error messages (e.g. [api errors](src/api/errors.ts) need to pass more info in the `Error.message` field, than just an error name.
- [ ] Chore: Upgrade dependencies (See *Dependabot* pull requests)
- [ ] Chore: Tests
  - Most importantly, integration tests for the [main.ts > run()](src/main.ts) logic.
  - N.B. Typescript (Strict) and yup (validation and type inference) already provide good type-safety guarantees.
- [ ] Chore: Publish the action to the [Actions Marketplace](https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace)

## Contributing:

See [CONTRIBUTING.md](CONTRIBUTING.md) for info on how to set up a local environment for development and tests.
