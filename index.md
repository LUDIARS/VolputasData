---
okf_version: "0.1"
---

# Voluptas private survey data

This private repository is the file authority for Voluptas local survey definitions and
responses. It is mounted by Voluptas as a Git submodule.

# Contents

* [Survey definitions](surveys/) - OKF documents generated from the versioned Voluptas questionnaire.
* [Responses](responses/) - one private branch per immutable GitHub user ID.

# Privacy boundary

* The repository must remain private.
* GitHub access tokens, OAuth tokens, email addresses, and unrelated profile fields must never be
  written here.
* A response branch is named `responses/github-<numeric-id>`. The response document records the
  immutable numeric ID and current GitHub login so login renames do not create a new identity.
* Survey answers may be sensitive. Do not merge response branches into `main`; grant repository
  access only to authorized reviewers.
* The [retention and deletion policy](POLICY.md) is mandatory for real responses.
