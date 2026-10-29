# pactwright-evidence

Testnet evidence store for the Pactwright verifier
([Pactwright-Kit](https://github.com/Pactwright/Pactwright-Kit) `services/verifier`).

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

An evidence item then uses the relative URI `<pact_id>/<sha256>`.

## Limits

- **Everything here is public.** Use it for testnet and demo deliveries only, never for private
  data. Mainnet needs private object storage with signed, expiring read URLs.
- Only Pactwright maintainers can write here; outside buyers can't upload yet.
- Files over 10 MB are refused by the verifier.
