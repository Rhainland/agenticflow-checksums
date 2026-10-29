# AgenticFlow release checksums

The SHA-256 of every release of the `agenticflow` tool that AgenticFlow's runners and workspace servers install, and the public key releases are signed with. Nothing else: no code.

They are kept here, outside AgenticFlow, so you can check a release against something whoever runs an AgenticFlow server can't change.

## Check a release before you install it

The Runners and Servers pages in AgenticFlow give you a command that downloads a release and checks it against a checksum. Before you run it, compare that checksum with the line for the same version in [`SHA256SUMS`](SHA256SUMS). If they differ, don't run it.

To check a file you already downloaded:

```bash
grep agenticflow-0.8.0.tgz SHA256SUMS | sha256sum -c -      # Linux
grep agenticflow-0.8.0.tgz SHA256SUMS | shasum -a 256 -c -  # macOS
```

## Check a signature

Each release is signed with an Ed25519 key whose private half exists only in the release workflow. The public half is [`release-key.pem`](release-key.pem). The tool carries the same key and uses it for `agenticflow update`. To check a release yourself:

```bash
openssl pkeyutl -verify -pubin -inkey release-key.pem -rawin \
    -in agenticflow-0.8.0.tgz -sigfile agenticflow-0.8.0.tgz.sig
```
