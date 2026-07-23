---
type: "Data Governance Policy"
title: "Voluptas survey data retention and deletion"
description: "Ownership, access, retention, deletion, and incident rules for private survey responses."
tags:
  - "voluptas"
  - "survey"
  - "privacy"
okf_version: "0.1"
---

# Survey data retention and deletion policy

Policy version: 1.0

Effective date: 2026-07-23

Owner: administrators of `LUDIARS/Voluptas-Data`

## Scope and purpose

This repository stores only Voluptas survey definitions and responses needed to analyze game
preferences. A response may contain sensitive opinions. It must not be reused for an unrelated
purpose without a separately reviewed policy.

Allowed response metadata is limited to the immutable GitHub numeric user ID, the current GitHub
login snapshot, submission time, Voluptas producer revision, survey version, and answers. Tokens,
email addresses, OAuth payloads, and unrelated GitHub profile fields are prohibited.

## Access

Keep the repository private. Repository administrators grant access only to people who need the
responses for the stated purpose and review repository access at least quarterly. Response
branches must never be merged into `main`.

## Retention

Delete a response branch at the earlier of:

1. 365 days after its most recent survey submission; or
2. an authenticated deletion request from the GitHub user represented by the branch.

Repository administrators review response branches at least quarterly. A deletion request must
be completed within 30 days after the requester is authenticated by their GitHub numeric user ID.

## Deletion runbook

The response branch is `responses/github-<numeric-id>`. Confirm the exact numeric ID, then remove
that exact remote branch and any authorized local copy:

```text
git push origin --delete responses/github-<numeric-id>
git branch --delete --force responses/github-<numeric-id>
git remote prune origin
```

Never use a wildcard or delete `main`. A file-deletion commit is insufficient because earlier
response commits remain reachable from the response branch history.

Deleting a branch removes its normal Git reference but does not guarantee immediate erasure of
unreachable Git objects, GitHub caches, audit records, or backups. For a verified full-erasure
request, a LUDIARS organization owner must escalate to GitHub Support and the applicable backup
owner, then record completion without copying the response content into the record.

## Incident handling

If a response reaches a public repository, log, pull request, issue, or unauthorized remote:

1. stop further publication;
2. remove public references without reproducing the response in tickets or chat;
3. rotate any exposed credential, if applicable;
4. notify a LUDIARS organization owner; and
5. use GitHub Support when history or cache removal is required.
