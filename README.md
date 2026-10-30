# pactwright-evidence

Testnet evidence store for the Pactwright verifier
([Pactwright-Kit](https://github.com/Pactwright/Pactwright-Kit) `services/verifier`). How the
verifier uses it: [Run a verifier → Evidence](https://pactwright.github.io/docs/guides/verifier/#evidence).

The verifier's `EVIDENCE_BUCKET_URL` points at this repository's raw files:

```
https://raw.githubusercontent.com/Pactwright/pactwright-evidence/main/
```

The verifier fetches evidence **only** from under that prefix. An evidence URI that resolves
anywhere else is refused, so a request can't make the verifier fetch arbitrary URLs. Every
blob's sha256 is checked against the evidence item before the model reads it, so a file here
can't be swapped for another without the verdict failing.

## Layout

```
<pact_id>/<sha256 of the file>
```

An evidence item then uses the relative URI `<pact_id>/<sha256>`. Each folder here is one pact; the
first, `40725564…`, holds the source and the delivered translation from the run in which the hosted
verifier's verdict was accepted on-chain
([the pact in Studio](https://pactwright-studio-testnet.onrender.com/pact/4072556402d709463f7cb888a4a9e03b061d906f0b7ca5c49ebb2eec4e7d5c55)). The
other folders come from local test runs against a separate demo instance of the contract
(`CC24GJO3…BE3X`), so they don't appear in Studio.

## Limits

- **Everything here is public.** Use it for testnet and demo deliveries only, never for private
  data. Mainnet needs private object storage with signed, expiring read URLs.
- Only Pactwright maintainers can write here; outside buyers can't upload yet.
- Files over 10 MB are refused by the verifier.
