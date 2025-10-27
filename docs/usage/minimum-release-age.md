# Minimum Release Age

`minimumReleaseAge` is a feature to require Renovate to wait for an amount of time before suggesting a dependency update.

If `minimumReleaseAge` is set to a time duration _and_ the update has a release timestamp header, then Renovate will check if the set duration has passed.

The use of `minimumReleaseAge` is not to slow down fast releasing project updates, but to provide a means to reduce risk supply chain security risks.

For example, `minimumReleaseAge=14 days` would ensure that a package update is not suggested by Renovate until 14 days after its release, which allows plenty of time to be scanned by malware scanners.

Note: Renovate will wait for the set duration to pass for each **separate** version.
Renovate does not wait until the package has seen no releases for x time-duration(`minimumReleaseAge`).

When the time passed since the release is _less_ than the set `minimumReleaseAge`: Renovate adds a "pending" status check to that update's branch.
After enough days have passed: Renovate replaces the "pending" status with a "passing" status check.

The datasource that Renovate uses must have a release timestamp for the `minimumReleaseAge` config option to work.
Some datasources may have a release timestamp, but in a format Renovate does not support.
In those cases a feature request needs to be implemented.

## Configuration options

The following configuration options can be used to enable and tune the functionality of Minimum Release Age:

- [`minimumReleaseAge`]
- [`minimumReleaseAgeBehaviour`]

## Interoperability with package managers

A number of**??** -

| Manager | Integrates |
| ------- | ---------- |
| pnpm    |            |
| Yarn    |            |

## Watch out

- missing
- **??**
- optional

## FAQs

### What happens if the datasource and/or registry does not provide a release timestamp, when **??**

!!! warning
TODO

Prior to Renovate 42, **??**.

Users of **??** are recommended to set **??** (added in 41.150.0) **??**

As of [the upcoming Renovate 42 release](https://github.com/renovatebot/renovate/discussions/38841) **??**.

### What happens when an update is not yet passing the minimum release age checks?

If a **??**, it will be found under the Dependency Dashboard in the "Pending Status Checks" and **??**.

You can **??** by enabling the Dependency Dashboard, or if you are self-hosting, you can use the [`checkedBranches`](https://docs.renovatebot.com/self-hosted-configuration/#checkedbranches) to force the **??**

### Which datasources support `minimumReleaseAge`?

You can confirm if your datasource supports the release timestamp by viewing [the documentation for the given datasource](./modules/datasource/index.md).

Note that you will also need to verify if the registry you're using **??**.

### Which registries support `minimumReleaseAge`?

We do not currently have an exhaustive list of registries **??**

You can also confirm - based on your debug logs -**??** via jkjk

### How do I **??**?

#### Maven

For `minimumReleaseAge` to work, the Maven source must return reliable `last-modified` headers.

<!-- markdownlint-disable MD046 -->

If your custom Maven source registry is **pull-through** and does _not_ support the `last-modified` header, like GAR (Google Artifact Registry's Maven implementation) then you can extend the Maven source registry URL with `https://repo1.maven.org/maven2` as the first item. Then the `currentVersionTimestamp` via `last-modified` will be taken from Maven central for public dependencies.

```json
"registryUrls": [
  "https://repo1.maven.org/maven2",
  "https://europe-maven.pkg.dev/org-artifacts/maven-virtual"
],
```
