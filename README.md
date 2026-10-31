<p align="center">
  <b>Testnet evidence for the Pactwright verifier</b><br>
  The exact bytes a verdict was based on, addressed by their SHA-256 and served read-only.
</p>

<p align="center">
  <a href="https://pactwright.github.io/docs/guides/verifier/"><b>Verifier guide</b></a> ·
  <a href="https://github.com/Pactwright/Pactwright-Kit"><b>Pactwright-Kit</b></a> ·
  <a href="https://pactwright-studio-testnet.onrender.com"><b>Studio</b></a>
</p>

> [!IMPORTANT]
> **Testnet and demo deliveries only.** Every file here is public, so nothing private belongs in it.
> Mainnet needs private object storage with signed, expiring read URLs.

## Contents

1. [Overview](#-overview)
2. [How the verifier reads it](#-how-the-verifier-reads-it)
3. [Layout](#️-layout)
4. [Limits](#️-limits)
5. [Community & Maintainers](#-community--maintainers)
6. [License](#license)

## 📖 Overview

Pactwright asks a verifier to check that a purchase was delivered as the condition describes. The
verifier's verdict has to be reproducible, so the verifier keeps the bytes it judged and names them
by hash. This repository is that store: the source document and the delivered file for each pact.

It is a data repository. There is no code here, no build and no tests; the verifier that reads it
lives in [`Pactwright-Kit`](https://github.com/Pactwright/Pactwright-Kit) under `services/verifier`,
and its guide is [Run a verifier → Evidence](https://pactwright.github.io/docs/guides/verifier/#evidence).

## 🔐 How the verifier reads it

The verifier's `EVIDENCE_BUCKET_URL` points at this repository's raw files:

```
https://raw.githubusercontent.com/Pactwright/pactwright-evidence/main/
```

Two rules make the store safe to publish:

- **One prefix only.** The verifier fetches evidence only from under that prefix. An evidence URI
  that resolves anywhere else is refused, so a request cannot make the verifier fetch arbitrary URLs.
- **Hash first, then read.** Every blob's SHA-256 is checked against the evidence item before the
  model sees it, so a file here cannot be swapped for another without the verdict failing.

## 🏗️ Layout

```
<pact_id>/<sha256 of the file>
```

An evidence item uses the relative URI `<pact_id>/<sha256>`. Each folder is one pact:

| Folder | What it holds |
|---|---|
| `40725564…` | The source and the delivered Portuguese translation from the run in which the hosted verifier's verdict was accepted on-chain. The pact is public in Studio: [`40725564…5c55`](https://pactwright-studio-testnet.onrender.com/pact/4072556402d709463f7cb888a4a9e03b061d906f0b7ca5c49ebb2eec4e7d5c55) |
| `7827891…`, `7fc320c…`, `cf40f14…` | Local test runs against a separate demo instance of the contract (`CC24GJO3…BE3X`), so they do not appear in Studio |

## ⚠️ Limits

- **Everything here is public.** Testnet and demo deliveries only, never private data.
- **Only Pactwright maintainers can write here.** Outside buyers cannot upload yet.
- **Files over 10 MB are refused** by the verifier.

## 🤝 Community & Maintainers

<!-- socials: add links when available -->

Questions and bug reports about the verifier go to
[`Pactwright-Kit` issues](https://github.com/Pactwright/Pactwright-Kit/issues).

## License

This repository has no `LICENSE` file: it holds testnet evidence data, not software. The code that
writes and reads it is [Pactwright-Kit](https://github.com/Pactwright/Pactwright-Kit), under
[Apache-2.0](https://github.com/Pactwright/Pactwright-Kit/blob/main/LICENSE).
