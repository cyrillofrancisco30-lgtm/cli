gh attestation verify ./gh-release.zip \
  --repo cli/cli \
  --signer-workflow cli/cli/.github/workflows/deployment.yml \
  --cert-oidc-issuer https://token.actions.githubusercontent.com \
  --predicate-type https://slsa.dev/provenance/v1 \
  --format json > verification.json


O material consolida uma distinção importante para o XA-TRUST: identificar uma execução concreta, verificar seus resultados e promover uma claim são operações diferentes; a verificação global E8 acrescenta uma camada de avaliação sobre o conjunto de claims.

O texto do README do `Azure/arm-ttk` também fornece contexto funcional: o projeto testa templates ARM quanto a práticas recomendadas, segurança e consistência de implementação. Ele descreve testes locais e sua execução no pipeline de CI. Isso caracteriza a finalidade do projeto, mas não substitui os resultados de uma execução específica.

### Consolidação do modelo XA-TRUST

| Etapa                         | Evidência ou condição central                                                                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| E3 — EXECUTION_EVENT_EVIDENCE | Identidade da execução, repositório, workflow, run_id, run_attempt, head_sha e contexto temporal                                               |
| E4 — OBSERVED_RESULT_EVIDENCE | Resultados concretos de jobs, steps e testes                                                                                                   |
| E5 — CRYPTOGRAPHIC_BINDING    | Integridade e vínculo criptográfico dos artefatos                                                                                              |
| E6 — INDEPENDENT_VERIFICATION | Verificação independente de identidade, proveniência, integridade e semântica pertinente à claim                                               |
| E7 — CLAIM-SCOPED VERIFIED    | Promoção da claim específica conforme os critérios e a política aplicáveis                                                                     |
| E8 — GLOBAL_VERIFIED          | Avaliação global com escopo definido, cobertura/completude, reconstrução independente, recálculo, correspondência exata e política de promoção |

A transição para E8 está explicitamente descrita no commit já examinado. Isso é evidência do modelo arquitetural global documentado, não apenas de uma sequência de execução local.

### Aplicação ao workflow do arm-ttk

O registro previamente identificado para `RunPester`, execução `37121498615`, tem `status=completed` e `conclusion=action_required`. Portanto, ele evidencia uma execução concluída com essa conclusão registrada. Não permite, isoladamente, atribuir `TEST_PASSED`, `E7_VERIFIED` ou `E8_GLOBAL_VERIFIED`.

Referências:

* [Execução RunPester #37121498615](https://github.com/Azure/arm-ttk/actions/runs/37121498615?utm_source=chatgpt.com)

* [Commit que documenta o modelo E7 → E8](https://github.com/Azure/arm-ttk/commit/21f85fbf49ba0fd463df336552a98a8d32fe37f0?utm_source=chatgpt.com)

Conclusão: o modelo XA-TRUST diferencia identidade de execução, resultados observados, vínculo criptográfico, verificação independente e promoção de claims. A extensão E8 formaliza a avaliação global. O próximo passo probatório é vincular uma execução concreta aos seus resultados e artefatos e, para E8, registrar a avaliação global correspondente.



# GitHub CLI

GitHub CLI, or the gh CLI, is GitHub on the command line. It brings pull requests, issues, and other GitHub concepts to the terminal next to where you are already working with `git` and your code.

> [!IMPORTANT]
> GitHub CLI's PGP signing key rotation for Linux package repositories is effective September 5, 2026; users experiencing package installation or update problems can find solutions in the [public announcement](https://github.com/cli/cli/issues/13118).

![screenshot of gh pr status](https://user-images.githubusercontent.com/98482/84171218-327e7a80-aa40-11ea-8cd1-5177fc2d0e72.png)

GitHub CLI is supported for users on GitHub.com, GitHub Enterprise Cloud, and [supported GitHub Enterprise Server versions](https://docs.github.com/en/enterprise-server/admin/all-releases), with support for macOS, Windows, and Linux.

## Documentation

For [installation options see below](#installation), for usage instructions [see the manual](https://cli.github.com/manual/).

## Agent skills

An [agent skill](https://agentskills.io) is available for driving `gh` from coding agents. Install or update it with the built-in `gh skill` command:

```shell
# Install the skill (user scope recommended)
gh skill install cli/cli gh --scope user

# Update the skill after a `gh` release
gh skill update gh
```

## Contributing

If anything feels off or if you feel that some functionality is missing, please check out the [contributing page](.github/CONTRIBUTING.md). There you will find instructions for sharing your feedback, building the tool locally, and submitting pull requests to the project.

If you are a hubber and are interested in shipping new commands for the CLI, check out our [doc on internal contributions](docs/working-with-us.md)

<!-- this anchor is linked to from elsewhere, so avoid renaming it -->
## Installation

### [macOS](docs/install_macos.md)

- [Homebrew](docs/install_macos.md#homebrew)
- [Precompiled binaries](docs/install_macos.md#precompiled-binaries) on [releases page][]

For additional macOS packages and installers, see [community-supported docs](docs/install_macos.md#community-unofficial)

### [Linux & Unix](docs/install_linux.md)

- [Debian, Raspberry Pi, Ubuntu](docs/install_linux.md#debian)
- [Amazon Linux, CentOS, Fedora, openSUSE, RHEL, SUSE](docs/install_linux.md#rpm)
- [Precompiled binaries](docs/install_linux.md#precompiled-binaries) on [releases page][]

For additional Linux & Unix packages and installers, see [community-supported docs](docs/install_linux.md#community-unofficial)

### [Windows](docs/install_windows.md)

- [WinGet](docs/install_windows.md#winget)
- [Precompiled binaries](docs/install_windows.md#precompiled-binaries) on [releases page][]

For additional Windows packages and installers, see [community-supported docs](docs/install_windows.md#community-unofficial)

### Build from source

See here on how to [build GitHub CLI from source](docs/install_source.md).

### GitHub Codespaces

To add GitHub CLI to your codespace, add the following to your [devcontainer file](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-features-to-a-devcontainer-file):

```json
"features": {
  "ghcr.io/devcontainers/features/github-cli:1": {}
}
```

### GitHub Actions

[GitHub-hosted runners](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) have the GitHub CLI pre-installed, which is updated weekly.

If a specific version is needed, your GitHub Actions workflow will need to install it based on the [macOS](#macos), [Linux & Unix](#linux--unix), or [Windows](#windows) instructions above.

For information on all pre-installed tools, see [`actions/runner-images`](https://github.com/actions/runner-images)

### Verification of binaries

Starting with v2.93.0, releases of `gh` are published as immutable releases. For more information, see [Immutable releases](https://docs.github.com/en/code-security/concepts/supply-chain-security/immutable-releases).

Since version 2.50.0, `gh` has been producing [Build Provenance Attestation](https://github.blog/changelog/2024-06-25-artifact-attestations-is-generally-available/), enabling a cryptographically verifiable paper-trail back to the origin GitHub repository, git revision, and build instructions used. The build provenance attestations are signed and rely on Public Good [Sigstore](https://www.sigstore.dev/) for PKI.

There are two common ways to verify a downloaded release, depending on whether `gh` is already installed or not. If `gh` is installed, it's trivial to verify a new release:

- **Option 1: Using `gh` if already installed:**

  ```shell
  $ gh at verify -R cli/cli gh_2.62.0_macOS_arm64.zip
  Loaded digest sha256:fdb77f31b8a6dd23c3fd858758d692a45f7fc76383e37d475bdcae038df92afc for file://gh_2.62.0_macOS_arm64.zip
  Loaded 1 attestation from GitHub API
  ✓ Verification succeeded!

  sha256:fdb77f31b8a6dd23c3fd858758d692a45f7fc76383e37d475bdcae038df92afc was attested by:
  REPO     PREDICATE_TYPE                  WORKFLOW
  cli/cli  https://slsa.dev/provenance/v1  .github/workflows/deployment.yml@refs/heads/trunk
  ```

- **Option 2: Using Sigstore [`cosign`](https://github.com/sigstore/cosign):**

  To perform this, download the [attestation](https://github.com/cli/cli/attestations) for the downloaded release and use cosign to verify the authenticity of the downloaded release:

  ```shell
  $ cosign verify-blob-attestation --bundle cli-cli-attestation-3120304.sigstore.json \
        --new-bundle-format \
        --certificate-oidc-issuer="https://token.actions.githubusercontent.com" \
        --certificate-identity="https://github.com/cli/cli/.github/workflows/deployment.yml@refs/heads/trunk" \
        gh_2.62.0_macOS_arm64.zip
  Verified OK
  ```

## Comparison with hub

For many years, [hub](https://github.com/github/hub) was the unofficial GitHub CLI tool. `gh` is a new project that helps us explore
what an official GitHub CLI tool can look like with a fundamentally different design. While both
tools bring GitHub to the terminal, `hub` behaves as a proxy to `git`, and `gh` is a standalone
tool. Check out our [more detailed explanation](docs/gh-vs-hub.md) to learn more.

[releases page]: https://github.com/cli/cli/releases/latest
[
{
"id": "24451280130",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1424356804,
"name": "cyrillofrancisco30-lgtm/cli",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli"
},
"payload": {
"repository_id": 1424356804,
"push_id": 46902505359,
"ref": "refs/heads/patch-2",
"head": "9c7bd5686b4679ceb4ee8b7e1ad70a54e3765519",
"before": "fa92838bef95fe4a29c1587693885d5e9bdb6cf1"
},
"public": true,
"created_at": "2026-10-18T12:49:04Z"
},
{
"id": "24438537488",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46881220768,
"ref": "refs/heads/master",
"head": "f4555f06bcb3be2a58f033ae30336bc938431e11",
"before": "9abbbda736f87b0b4ebe40498fc0ed3882a03bf1"
},
"public": true,
"created_at": "2026-10-18T06:46:58Z"
},
{
"id": "17530793091",
"type": "ForkEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 212613049,
"name": "cli/cli",
"url": "https://api.github.com/repos/cli/cli"
},
"payload": {
"action": "forked",
"forkee": {
"id": 1424356804,
"node_id": "R_kgDOVOX1xA",
"name": "cli",
"full_name": "cyrillofrancisco30-lgtm/cli",
"private": false,
"owner": {
"login": "cyrillofrancisco30-lgtm",
"id": 224322139,
"node_id": "U_kgDODV7iWw",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?v=4",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"html_url": "https://github.com/cyrillofrancisco30-lgtm",
"followers_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/followers",
"following_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/following{/other_user}",
"gists_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/gists{/gist_id}",
"starred_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/starred{/owner}{/repo}",
"subscriptions_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/subscriptions",
"organizations_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/orgs",
"repos_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/repos",
"events_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/events{/privacy}",
"received_events_url": "https://api.github.com/users/cyrillofrancisco30-lgtm/received_events",
"type": "User",
"user_view_type": "public",
"site_admin": false
},
"html_url": "https://github.com/cyrillofrancisco30-lgtm/cli",
"description": "GitHub’s official command line tool",
"fork": true,
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli",
"forks_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/forks",
"keys_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/keys{/key_id}",
"collaborators_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/collaborators{/collaborator}",
"teams_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/teams",
"hooks_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/hooks",
"issue_events_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/issues/events{/number}",
"events_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/events",
"assignees_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/assignees{/user}",
"branches_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/branches{/branch}",
"tags_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/tags",
"blobs_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/git/blobs{/sha}",
"git_tags_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/git/tags{/sha}",
"git_refs_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/git/refs{/sha}",
"trees_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/git/trees{/sha}",
"statuses_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/statuses/{sha}",
"languages_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/languages",
"stargazers_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/stargazers",
"contributors_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/contributors",
"subscribers_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/subscribers",
"subscription_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/subscription",
"commits_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/commits{/sha}",
"git_commits_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/git/commits{/sha}",
"comments_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/comments{/number}",
"issue_comment_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/issues/comments{/number}",
"contents_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/contents/{+path}",
"compare_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/compare/{base}...{head}",
"merges_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/merges",
"archive_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/{archive_format}{/ref}",
"downloads_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/downloads",
"issues_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/issues{/number}",
"pulls_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/pulls{/number}",
"milestones_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/milestones{/number}",
"notifications_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/notifications{?since,all,participating}",
"labels_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/labels{/name}",
"releases_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/releases{/id}",
"deployments_url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/cli/deployments",
"created_at": "2026-10-18T12:38:18Z",
"updated_at": "2026-10-18T12:38:18Z",
"pushed_at": "2026-10-18T13:04:04Z",
"git_url": "git://github.com/cyrillofrancisco30-lgtm/cli.git",
"ssh_url": "git@github.com:cyrillofrancisco30-lgtm/cli.git",
"clone_url": "https://github.com/cyrillofrancisco30-lgtm/cli.git",
"svn_url": "https://github.com/cyrillofrancisco30-lgtm/cli",
"homepage": "https://cli.github.com",
"size": 82406,
"stargazers_count": 0,
"watchers_count": 0,
"language": null,
"has_issues": false,
"has_projects": true,
"has_downloads": false,
"has_wiki": false,
"has_pages": false,
"has_discussions": false,
"forks_count": 0,
"mirror_url": null,
"archived": false,
"disabled": false,
"open_issues_count": 0,
"license": {
"key": "mit",
"name": "MIT License",
"spdx_id": "MIT",
"url": "https://api.github.com/licenses/mit",
"node_id": "MDc6TGljZW5zZTEz"
},
"allow_forking": true,
"is_template": false,
"web_commit_signoff_required": false,
"has_pull_requests": true,
"pull_request_creation_policy": "all",
"topics": [

],  
    "visibility": "public",  
    "forks": 0,  
    "open_issues": 0,  
    "watchers": 0,  
    "default_branch": "trunk"  
  }  
},  
"public": true,  
"created_at": "2026-10-18T12:38:18Z",  
"org": {  
  "id": 59704711,  
  "login": "cli",  
  "gravatar_id": "",  
  "url": "https://api.github.com/orgs/cli",  
  "avatar_url": "https://avatars.githubusercontent.com/u/59704711?"  
}

},
{
"id": "24284350442",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46657796283,
"ref": "refs/heads/patch-11",
"head": "ad5fdaa0afd1f72f4961ecdb1c359390ed32b1b6",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-10-15T23:54:13Z"
},
{
"id": "24274538620",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46665632614,
"ref": "refs/heads/master",
"head": "9abbbda736f87b0b4ebe40498fc0ed3882a03bf1",
"before": "05dac0034c3a4213c7caa71af6a63930cc80a860"
},
"public": true,
"created_at": "2026-10-16T01:52:49Z"
},
{
"id": "24274172873",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46665413961,
"ref": "refs/heads/master",
"head": "05dac0034c3a4213c7caa71af6a63930cc80a860",
"before": "7ece3230e21832b8dfc8ed4f7619b382cb2aa7ea"
},
"public": true,
"created_at": "2026-10-16T01:49:27Z"
},
{
"id": "24272198849",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46664118852,
"ref": "refs/heads/master",
"head": "7ece3230e21832b8dfc8ed4f7619b382cb2aa7ea",
"before": "4cb42c53c1d37b571fa89852e0ae5b6c3446bb07"
},
"public": true,
"created_at": "2026-10-16T01:29:37Z"
},
{
"id": "24242961508",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1370809373,
"name": "cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version"
},
"payload": {
"repository_id": 1370809373,
"push_id": 46668654504,
"ref": "refs/heads/main",
"head": "11d303834ba10acad64011d7288f7dfee41c9209",
"before": "7dced563a620e88856cb8463b392c33977abe633"
},
"public": true,
"created_at": "2026-10-16T02:38:35Z"
},
{
"id": "24209569968",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46661924960,
"ref": "refs/heads/patch-11",
"head": "98739dd09af552fbd031bd5316c0e30eee956b41",
"before": "ad5fdaa0afd1f72f4961ecdb1c359390ed32b1b6"
},
"public": true,
"created_at": "2026-10-16T00:56:21Z"
},
{
"id": "23992386862",
"type": "CreateEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"ref": "cyrillofrancisco30-lgtm-patch-5",
"ref_type": "branch",
"full_ref": "refs/heads/cyrillofrancisco30-lgtm-patch-5",
"master_branch": "master",
"description": null,
"pusher_type": "user"
},
"public": true,
"created_at": "2026-10-13T04:54:05Z"
},
{
"id": "23973049389",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 46288977154,
"ref": "refs/heads/main",
"head": "7e6b7d15ae67eb7fd8c1017319e298232e709890",
"before": "cbfd62af7eb40794fc1e47a4a1f09d213df5e363"
},
"public": true,
"created_at": "2026-10-13T00:46:19Z"
},
{
"id": "23967314086",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46312748278,
"ref": "refs/heads/master",
"head": "4cb42c53c1d37b571fa89852e0ae5b6c3446bb07",
"before": "09ce7a31ef2e2d72d67674604d05b2df5e1edfc3"
},
"public": true,
"created_at": "2026-10-13T06:47:53Z"
},
{
"id": "23934093492",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 46288833879,
"ref": "refs/heads/main",
"head": "cbfd62af7eb40794fc1e47a4a1f09d213df5e363",
"before": "8f5f585dc09c526786bb206a170638cb60186979"
},
"public": true,
"created_at": "2026-10-13T00:43:58Z"
},
{
"id": "23840207737",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46304859988,
"ref": "refs/heads/master",
"head": "09ce7a31ef2e2d72d67674604d05b2df5e1edfc3",
"before": "ff640d8106ad99bcc36dff9c013bc0beae8b3740"
},
"public": true,
"created_at": "2026-10-13T04:57:17Z"
},
{
"id": "23825402536",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 46289185463,
"ref": "refs/heads/main",
"head": "1903e088c590805e507e76b8c6dff16c096ad3b9",
"before": "7e6b7d15ae67eb7fd8c1017319e298232e709890"
},
"public": true,
"created_at": "2026-10-13T00:49:50Z"
},
{
"id": "23824946621",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 46288726737,
"ref": "refs/heads/main",
"head": "8f5f585dc09c526786bb206a170638cb60186979",
"before": "17943c7b1e909b70ac38c560e89c590644526fd3"
},
"public": true,
"created_at": "2026-10-13T00:42:09Z"
},
{
"id": "23718556074",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1370809373,
"name": "cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version"
},
"payload": {
"repository_id": 1370809373,
"push_id": 46020710103,
"ref": "refs/heads/main",
"head": "7dced563a620e88856cb8463b392c33977abe633",
"before": "2524afeb97089c54b88b38061f4ecb20f0c0e0a3"
},
"public": true,
"created_at": "2026-10-10T01:27:53Z"
},
{
"id": "23710407274",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46011707650,
"ref": "refs/heads/master",
"head": "90f3e741094e001c1db71abe96af3018cad0badd",
"before": "5a85e73cbcf159c7b55ec845c5fe0bf96b3dfc18"
},
"public": true,
"created_at": "2026-10-09T22:43:46Z"
},
{
"id": "23708643009",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46012554489,
"ref": "refs/heads/master",
"head": "adb4e5a16bbf347a716530474f3538a7b0f38136",
"before": "30a3e9eb54a22e2e583de2774558e7147e81733f"
},
"public": true,
"created_at": "2026-10-09T22:57:52Z"
},
{
"id": "23605030974",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1370809373,
"name": "cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version"
},
"payload": {
"repository_id": 1370809373,
"push_id": 46020501120,
"ref": "refs/heads/main",
"head": "2524afeb97089c54b88b38061f4ecb20f0c0e0a3",
"before": "be517a14aa8c83dc2bba0cbf45fba6b7181dd99b"
},
"public": true,
"created_at": "2026-10-10T01:23:43Z"
},
{
"id": "23600900090",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46013751601,
"ref": "refs/heads/master",
"head": "ff640d8106ad99bcc36dff9c013bc0beae8b3740",
"before": "adb4e5a16bbf347a716530474f3538a7b0f38136"
},
"public": true,
"created_at": "2026-10-09T23:17:50Z"
},
{
"id": "23593940323",
"type": "CreateEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"ref": "cyrillofrancisco30-lgtm-patch-4",
"ref_type": "branch",
"full_ref": "refs/heads/cyrillofrancisco30-lgtm-patch-4",
"master_branch": "master",
"description": null,
"pusher_type": "user"
},
"public": true,
"created_at": "2026-10-09T18:52:23Z"
},
{
"id": "23591136266",
"type": "CreateEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"ref": "cyrillofrancisco30-lgtm-patch-3",
"ref_type": "branch",
"full_ref": "refs/heads/cyrillofrancisco30-lgtm-patch-3",
"master_branch": "master",
"description": null,
"pusher_type": "user"
},
"public": true,
"created_at": "2026-10-09T18:38:28Z"
},
{
"id": "23534427209",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 46012272424,
"ref": "refs/heads/master",
"head": "30a3e9eb54a22e2e583de2774558e7147e81733f",
"before": "90f3e741094e001c1db71abe96af3018cad0badd"
},
"public": true,
"created_at": "2026-10-09T22:53:07Z"
},
{
"id": "23253265892",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 45695924431,
"ref": "refs/heads/main",
"head": "17943c7b1e909b70ac38c560e89c590644526fd3",
"before": "5f483e19958d89ffc2d0c3caf02b703a03993857"
},
"public": true,
"created_at": "2026-10-07T05:17:44Z"
},
{
"id": "23241429644",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 45695685165,
"ref": "refs/heads/main",
"head": "5f483e19958d89ffc2d0c3caf02b703a03993857",
"before": "b536f130faca254604143842fe0f58eccfaa20c8"
},
"public": true,
"created_at": "2026-10-07T05:14:03Z"
},
{
"id": "23028236606",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 45342335654,
"ref": "refs/heads/main",
"head": "6ff5bbc16db3fd11c472407755bf263a35a70907",
"before": "59ed6586b65c6fc1b40b8e6c08333b3c349aad42"
},
"public": true,
"created_at": "2026-10-03T13:17:25Z"
},
{
"id": "23025594064",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1339873593,
"name": "cyrillofrancisco30-lgtm/arm-ttk",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk"
},
"payload": {
"repository_id": 1339873593,
"push_id": 45351681876,
"ref": "refs/heads/master",
"head": "5a85e73cbcf159c7b55ec845c5fe0bf96b3dfc18",
"before": "32583a772601ceb8cbf10bfc5372c4062166d04b"
},
"public": true,
"created_at": "2026-10-03T15:56:42Z"
},
{
"id": "23020807120",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1370809373,
"name": "cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/Az-Get-Resource-API-Version"
},
"payload": {
"repository_id": 1370809373,
"push_id": 45334512163,
"ref": "refs/heads/main",
"head": "bcfa73f0457009f9a417fb508a5df7d63613fc32",
"before": "dc54d49d487ffcf45b6e3467a4bc4c53d0734dce"
},
"public": true,
"created_at": "2026-10-03T10:49:45Z"
},
{
"id": "22937635639",
"type": "PushEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 1381490885,
"name": "cyrillofrancisco30-lgtm/github-artifact-exporter",
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/github-artifact-exporter"
},
"payload": {
"repository_id": 1381490885,
"push_id": 45267532664,
"ref": "refs/heads/main",
"head": "59ed6586b65c6fc1b40b8e6c08333b3c349aad42",
"before": "29f6895ac3174c5b66ddb47075aa3361412443cd"
},
"public": true,
"created_at": "2026-10-02T15:44:31Z"
}
]