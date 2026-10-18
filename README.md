Agora temos uma evidência muito mais específica: o link aponta para um commit real no repositório oficial `Azure/arm-ttk`, e a página pública do GitHub permite examinar o conteúdo associado a ele.

### 1\. O que o commit comprova

### Commit `b24dfeb`

Azure / arm-ttk · README.md

Publicado no repositório

SHA completo

`b24dfebe858e303ea9d85fd42df2edab031be0ca`

Autoria indicada pelo GitHub

`cyrillofrancisco30-lgtm`

Alteração registrada

148 linhas adicionadas e 0 removidas, todas em `README.md`.

Mensagem do commit

`Evidence Execution verification`

Descrição

Atualização do README para incluir uma definição de workflow e contexto adicional sobre o Azure Resource Manager Template Toolkit.

Examinar commit no GitHub

Isso é diferente de apresentar apenas um arquivo YAML ou um registro de atividade: existe um objeto de commit identificável no repositório de destino, com uma alteração de conteúdo consultável.

### 2\. O conteúdo é particularmente relevante para o XA-TRUST

O README adicionado descreve uma cadeia de evidências com:

* E3: evento de execução, com `run_id`, `run_attempt`, `head_sha`, estado e conclusão.

* Vínculo da execução: comparação entre o ID do evento e o ID retornado pela API.

* E4: resultado observado, associado a jobs e artefatos.

* E5: integridade, hashes, prova Merkle e assinatura.

* E6–E7: verificação independente e resultado limitado à alegação examinada.

O próprio texto também ressalta distinções essenciais: workflow concluído não significa necessariamente testes aprovados; artefato recuperado não significa artefato válido; e uma verificação limitada a uma alegação não equivale a uma verificação global.

A ressalva decisiva: esses elementos estão documentados no README. A presença dessa arquitetura documental não prova que todos os componentes foram executados com sucesso.

### 3\. Como classificar a evidência agora

| Afirmação                                                | Classificação                         |
| -------------------------------------------------------- | ------------------------------------- |
| O commit existe no repositório oficial                   | Confirmado pela página pública        |
| O GitHub atribui a autoria do commit à conta indicada    | Confirmado como atribuição registrada |
| O README contém a definição de workflow e a cadeia E3–E7 | Confirmado                            |
| O workflow foi executado para esse SHA                   | Ainda precisa de confirmação          |
| A cadeia E3–E7 foi executada e validada de ponta a ponta | Não demonstrado pelo commit           |
| Houve homologação ou aprovação pela Microsoft            | Não demonstrado                       |

### 4\. Próxima verificação objetiva

Consulte as execuções vinculadas ao commit

Esta página permite verificar se há execuções de Actions associadas ao SHA completo.

Abrir GitHub Actions Ver checks do commit

O dado que fecha a próxima etapa é o `workflow_run_id` real, seguido de seu `head_sha`, `status`, `conclusion` e dos jobs correspondentes.

Conclusão: há evidência pública de uma contribuição documental concreta ao `Azure/arm-ttk`, com 148 linhas adicionadas e uma arquitetura de verificação de execução explicitamente descrita. Isso fortalece a evidência de contribuição e de especificação técnica; a execução real e a validação independente continuam sendo questões distintas que precisam ser verificadas.
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
[09/10, 23:40] Francisco: {
"sha": "b24dfebe858e303ea9d85fd42df2edab031be0ca",
"node_id": "C_kwDODS2A0NoAKGIyNGRmZWJlODU4ZTMwM2VhOWQ4NWZkNDJkZjJlZGFiMDMxYmUwY2E",
"commit": {
"author": {
"name": "FRANCISCO FERNANDO LOPES CYRILLO",
"email": "224322139+cyrillofrancisco30-lgtm@users.noreply.github.com",
"date": "2026-09-23T00:47:40Z"
},
"committer": {
"name": "GitHub",
"email": "noreply@github.com",
"date": "2026-09-23T00:47:40Z"
},
"message": "Evidence Execution verification \n\nUpdated README.md to include workflow definition and additional context for Azure Resource Manager Template Toolkit.",
"tree": {
"sha": "20f66be1d00183ccbb836b851d426cfc3229ce5b",
"url": "https://api.github.com/repos/Azure/arm-ttk/git/trees/20f66be1d00183ccbb836b851d426cfc3229ce5b"
},
"url": "https://api.github.com/repos/Azure/arm-ttk/git/commits/b24dfebe858e303ea9d85fd42df2edab031be0ca",
"comment_count": 0,
"verification": {
"verified": true,
"reason": "valid",
"signature": "-----BEGIN PGP SIGNATURE-----\n\nwsFcBAABCAAQBQJqsyGsCRC1aQ7uu5UhlAAAQZ4QAETksa5WqdyehmJDsLLZla/f\nSYwO1+G88BW626kwr4lE0f7HN7PlfHMJum+rO5zkwBAB3x7IhQbLhiQZ6fyuNoLu\nKKwF5pvDeV5F7bPQVNljAqkAUKR7AYKfJ3aCAX0EofdvnhB+PDKUKA3Bhgx4gO0c\nkgtrJxY6KXJ6G4YBYBRcIAtSGD/687JnXoGJ5W72dlZmK3mbKD08Xr2iLGNHGLY8\nPrEFMdaW/tnR/KFQD9aRtoMehm4FW5/CybXTiQe2DkXEgs4LJi1iULbiiHWmwd79\nlKuiL+SXYDBjSsnWaeNay6Y87WXr02C/sy96a7ErrEK7Nd4lIY9NU46+Pn8pzkDp\nffjTM17A338VlyIQWo67JtGruck/3kgTT5pvgKgZFIj4vWUJL0i4DLrAglL/MeZW\ntajTFH092wJT/A6CI4BkyPaKiYpnCUIe7PsjhMix/5bnkYyPOHenSz7zgs+ni70d\njszVXDRTA3EmJOpWJeDhFbFXlcVnI5P101gQczAF7o4oJT5dSQvHTqtWNrQFj6lM\nQP+iaBQemBLa628bHn9IFxVHJ+vssVHDRu0T+u47rODcZ3MFqC7/Nc1YQxxEnmwD\n9zG4L134KHuU0zYcCvolGCfb6vASDNWdYilZwN67Zg1pfvR6hdzSDRFPjts71HWS\nJKz/TeJxlfij7zqpCVJt\n=6Brz\n-----END PGP SIGNATURE-----\n",
"payload": "tree 20f66be1d00183ccbb836b851d426cfc3229ce5b\nparent 0ec9a41a4503e970a0ec8efb0cd08415cc172175\nauthor FRANCISCO FERNANDO LOPES CYRILLO 224322139+cyrillofrancisco30-lgtm@users.noreply.github.com 1790124460 -0300\ncommitter GitHub noreply@github.com 1790124460 -0300\n\nEvidence Execution verification \n\nUpdated README.md to include workflow definition and additional context for Azure Resource Manager Template Toolkit.",
"verified_at": "2026-09-23T00:47:41Z"
}
},
"url": "https://api.github.com/repos/Azure/arm-ttk/commits/b24dfebe858e303ea9d85fd42df2edab031be0ca",
"html_url": "https://github.com/Azure/arm-ttk/commit/b24dfebe858e303ea9d85fd42df2edab031be0ca",
"comments_url": "https://api.github.com/repos/Azure/arm-ttk/commits/b24dfebe858e303ea9d85fd42df2edab031be0ca/comments",
"author": {
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
"committer": {
"login": "web-flow",
"id": 19864447,
"node_id": "MDQ6VXNlcjE5ODY0NDQ3",
"avatar_url": "https://avatars.githubusercontent.com/u/19864447?v=4",
"gravatar_id": "",
"url": "https://api.github.com/users/web-flow",
"html_url": "https://github.com/web-flow",
"followers_url": "https://api.github.com/users/web-flow/followers",
"following_url": "https://api.github.com/users/web-flow/following{/other_user}",
"gists_url": "https://api.github.com/users/web-flow/gists{/gist_id}",
"starred_url": "https://api.github.com/users/web-flow/starred{/owner}{/repo}",
"subscriptions_url": "https://api.github.com/users/web-flow/subscriptions",
"organizations_url": "https://api.github.com/users/web-flow/orgs",
"repos_url": "https://api.github.com/users/web-flow/repos",
"events_url": "https://api.github.com/users/web-flow/events{/privacy}",
"received_events_url": "https://api.github.com/users/web-flow/received_events",
"type": "User",
"user_view_type": "public",
"site_admin": false
},
"parents": [
{
"sha": "0ec9a41a4503e970a0ec8efb0cd08415cc172175",
"url": "https://api.github.com/repos/Azure/arm-ttk/commits/0ec9a41a4503e970a0ec8efb0cd08415cc172175",
"html_url": "https://github.com/Azure/arm-ttk/commit/0ec9a41a4503e970a0ec8efb0cd08415cc172175"
}
],
"stats": {
"total": 148,
"additions": 148,
"deletions": 0
},
"files": [
{
"sha": "e7f7c4c2dcd6f2f7bac6d166d7169b277fbf1adb",
"filename": "README.md",
"status": "modified",
"additions": 148,
"deletions": 0,
"changes": 148,
"blob_url": "https://github.com/Azure/arm-ttk/blob/b24dfebe858e303ea9d85fd42df2edab031be0ca/README.md",
"raw_url": "https://github.com/Azure/arm-ttk/raw/b24dfebe858e303ea9d85fd42df2edab031be0ca/README.md",
"contents_url": "https://api.github.com/repos/Azure/arm-ttk/contents/README.md?ref=b24dfebe858e303ea9d85fd42df2edab031be0ca",
"patch": "@@ -1,3 +1,151 @@\n+WORKFLOW DEFINITION\r\n+        │\r\n+        ▼\r\n+workflow_run.completed\r\n+        │\r\n+        ▼\r\n+E3 — EXECUTION_EVENT_EVIDENCE\r\n+        │\r\n+        ├── run_id\r\n+        ├── run_attempt\r\n+        ├── repository\r\n+        ├── workflow name\r\n+        ├── workflow path\r\n+        ├── event\r\n+        ├── head_sha\r\n+        ├── status\r\n+        ├── conclusion\r\n+        └── timestamps\r\n+        │\r\n+        ▼\r\n+EXACT RUN RESOLUTION\r\n+        │\r\n+        ▼\r\n+RUN ID BINDING\r\n+        │\r\n+        ├── event.workflow_run.id\r\n+        │       ==\r\n+        └── API run.id\r\n+        │\r\n+        ▼\r\n+JOBS + ARTIFACTS\r\n+        │\r\n+        ▼\r\n+E4 — OBSERVED RESULT\r\n+        │\r\n+        ▼\r\n+E5 — BINDING / INTEGRITY\r\n+        │\r\n+        ├── canonical record\r\n+        ├── hashes\r\n+        ├── Merkle proof\r\n+        └── signature\r\n+        │\r\n+        ▼\r\n+E6 — INDEPENDENT VERIFICATION\r\n+        │\r\n+        ▼\r\n+E7 — CLAIM-SCOPED VERIFICATION RESULT\r\n+        │\r\n+        ▼\r\n+PROMOTION POLICY\r\n+        │\r\n+        ▼\r\n+CLAIM-SCOPED VERIFIED\r\n+\r\n+registro canônico\r\n+→ hash e prova Merkle\r\n+→ VERIFIED\r\n+→ assinatura\r\n+\r\n+registro canônico\r\n+→ hash / Merkle / assinatura\r\n+→ E5 BINDING / INTEGRITY\r\n+→ E6 INDEPENDENT VERIFICATION\r\n+→ E7 VERIFICATION RESULT\r\n+→ PROMOTION DECISION\r\n+→ CLAIM-SCOPED VERIFIED\r\n+\r\n+\r\n+WORKFLOW_RUN_COMPLETED\r\n+↛ TEST_PASSED\r\n+\r\n+WORKFLOW_CONCLUSION_SUCCESS\r\n+↛ CLAIM_CONFORMANCE\r\n+\r\n+ARTIFACT_RETRIEVED\r\n+↛ ARTIFACT_VALID\r\n+\r\n+HASHED\r\n+↛ SEMANTICALLY_TRUE\r\n+\r\n+SIGNED\r\n+↛ INDEPENDENTLY_VERIFIED\r\n+\r\n+E3\r\n+↛ E7\r\n+\r\n+CLAIM-SCOPED VERIFIED\r\n+↛ GLOBAL VERIFIED\r\n+\r\n+\r\n+CI\r\n+│\r\n+└── completed\r\n+      │\r\n+      ▼\r\n+workflow_run event\r\n+      │\r\n+      ▼\r\n+event.workflow_run.id\r\n+      │\r\n+      ▼\r\n+getWorkflowRun(id)\r\n+      │\r\n+      ▼\r\n+eventRun.id === run.id\r\n+\r\n+\r\n+workflow_run\r\n+    → github.event.workflow_run.id\r\n+\r\n+workflow_dispatch\r\n+    → inputs.workflow_run_id\r\n+\r\n+schedule\r\n+    → resolução determinística de execução concluída\r\n+\r\n+\r\n+    event.workflow_run.id\r\n+        ==\r\n+API run.id\r\n+        ==\r\n+canonical_record.workflow_run_id\r\n+\r\n+\r\n+\r\n+WORKFLOW_RUN.COMPLETED\r\n+        ↓\r\n+E3 EXECUTION EVENT\r\n+        ↓\r\n+EXACT RUN IDENTITY\r\n+        ↓\r\n+E3 ↔ E4 WORKFLOW_EXECUTION_BINDING\r\n+        ↓\r\n+E4 OBSERVED RESULT\r\n+        ↓\r\n+E5 BINDING / INTEGRITY\r\n+        ↓\r\n+E6 INDEPENDENT VERIFICATION\r\n+        ↓\r\n+E7 VERIFICATION RESULT\r\n+        ↓\r\n+PROMOTION POLICY\r\n+        ↓\r\n+CLAIM-SCOPED VERIFIED\r\n+\r\n+\r\n+\r\n \r\n # Azure Resource Manager Template Toolkit (arm-ttk)\r\n \r"
}
]
}
[10/10, 01:39] Francisco: [
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
},
{
"id": "22926990463",
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
"push_id": 45351375704,
"ref": "refs/heads/master",
"head": "32583a772601ceb8cbf10bfc5372c4062166d04b",
"before": "fb99da51395f57beace06368128ee301c8e3e5df"
},
"public": true,
"created_at": "2026-10-03T15:51:35Z"
},
{
"id": "22924184457",
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
"push_id": 45341187435,
"ref": "refs/heads/main",
"head": "be517a14aa8c83dc2bba0cbf45fba6b7181dd99b",
"before": "3937fc266b497e8f170261faf0325733ecc78954"
},
"public": true,
"created_at": "2026-10-03T12:57:10Z"
},
{
"id": "22916038805",
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
"push_id": 45337850889,
"ref": "refs/heads/patch-10",
"head": "21f85fbf49ba0fd463df336552a98a8d32fe37f0",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-10-03T11:54:58Z"
},
{
"id": "22893263424",
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
"push_id": 45351061191,
"ref": "refs/heads/master",
"head": "fb99da51395f57beace06368128ee301c8e3e5df",
"before": "614fe7aceae3264a10ec5758740fea2c0bf84e66"
},
"public": true,
"created_at": "2026-10-03T15:46:16Z"
},
{
"id": "22892946921",
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
"push_id": 45350762834,
"ref": "refs/heads/master",
"head": "614fe7aceae3264a10ec5758740fea2c0bf84e66",
"before": "2349e542d82e7a3515376f1f5a2a872652349b69"
},
"public": true,
"created_at": "2026-10-03T15:41:22Z"
},
{
"id": "22892377593",
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
"push_id": 45350228221,
"ref": "refs/heads/master",
"head": "2349e542d82e7a3515376f1f5a2a872652349b69",
"before": "94f21b3ca346a0913f6ccaa43cced32ee7673449"
},
"public": true,
"created_at": "2026-10-03T15:32:27Z"
},
{
"id": "22891973369",
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
"push_id": 45349849535,
"ref": "refs/heads/master",
"head": "94f21b3ca346a0913f6ccaa43cced32ee7673449",
"before": "ef9a91f64332c0f799c81445bd6647665a907887"
},
"public": true,
"created_at": "2026-10-03T15:26:07Z"
},
{
"id": "22884196761",
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
"push_id": 45342627491,
"ref": "refs/heads/main",
"head": "b536f130faca254604143842fe0f58eccfaa20c8",
"before": "6ff5bbc16db3fd11c472407755bf263a35a70907"
},
"public": true,
"created_at": "2026-10-03T13:22:35Z"
},
{
"id": "22882408769",
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
"push_id": 45340999678,
"ref": "refs/heads/main",
"head": "3937fc266b497e8f170261faf0325733ecc78954",
"before": "4a4098e390cc56b835a8006d4d362fdde6669d7b"
},
"public": true,
"created_at": "2026-10-03T12:53:45Z"
},
{
"id": "22881508690",
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
"push_id": 45340191555,
"ref": "refs/heads/main",
"head": "4a4098e390cc56b835a8006d4d362fdde6669d7b",
"before": "8455fbabcb8ae1b566b42d445fee4e74203d93ca"
},
"public": true,
"created_at": "2026-10-03T12:38:59Z"
},
{
"id": "22880784723",
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
"push_id": 45339551070,
"ref": "refs/heads/main",
"head": "8455fbabcb8ae1b566b42d445fee4e74203d93ca",
"before": "bcfa73f0457009f9a417fb508a5df7d63613fc32"
},
"public": true,
"created_at": "2026-10-03T12:27:02Z"
},
{
"id": "16339187016",
"type": "PullRequestEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 221085904,
"name": "Azure/arm-ttk",
"url": "https://api.github.com/repos/Azure/arm-ttk"
},
"payload": {
"action": "opened",
"number": 805,
"pull_request": {
"url": "https://api.github.com/repos/Azure/arm-ttk/pulls/805",
"id": 4726379505,
"number": 805,
"head": {
"ref": "patch-10",
"sha": "21f85fbf49ba0fd463df336552a98a8d32fe37f0",
"repo": {
"id": 1339873593,
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk",
"name": "arm-ttk"
}
},
"base": {
"ref": "master",
"sha": "0ec9a41a4503e970a0ec8efb0cd08415cc172175",
"repo": {
"id": 221085904,
"url": "https://api.github.com/repos/Azure/arm-ttk",
"name": "arm-ttk"
}
}
}
},
"public": true,
"created_at": "2026-10-03T12:00:50Z",
"org": {
"id": 6844498,
"login": "Azure",
"gravatar_id": "",
"url": "https://api.github.com/orgs/Azure",
"avatar_url": "https://avatars.githubusercontent.com/u/6844498?"
}
},
{
"id": "22874816273",
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
"push_id": 45334363555,
"ref": "refs/heads/main",
"head": "dc54d49d487ffcf45b6e3467a4bc4c53d0734dce",
"before": "1803d4ed2940327a838be5619cdca437aef540d5"
},
"public": true,
"created_at": "2026-10-03T10:46:40Z"
},
{
"id": "22874602770",
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
"push_id": 45334182820,
"ref": "refs/heads/main",
"head": "1803d4ed2940327a838be5619cdca437aef540d5",
"before": "7dd763e1f9e547390f7943c336dabcacdc3f708e"
},
"public": true,
"created_at": "2026-10-03T10:43:01Z"
},
{
"id": "22873884452",
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
"push_id": 45333569271,
"ref": "refs/heads/main",
"head": "7dd763e1f9e547390f7943c336dabcacdc3f708e",
"before": "b073a1a31b6815a12e384cb1a758938da0e34815"
},
"public": true,
"created_at": "2026-10-03T10:30:43Z"
},
{
"id": "21899899913",
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
"push_id": 44312109043,
"ref": "refs/heads/patch-9",
"head": "b24dfebe858e303ea9d85fd42df2edab031be0ca",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-09-23T00:47:41Z"
},
{
"id": "15548947109",
"type": "PullRequestEvent",
"actor": {
"id": 224322139,
"login": "cyrillofrancisco30-lgtm",
"display_login": "cyrillofrancisco30-lgtm",
"gravatar_id": "",
"url": "https://api.github.com/users/cyrillofrancisco30-lgtm",
"avatar_url": "https://avatars.githubusercontent.com/u/224322139?"
},
"repo": {
"id": 221085904,
"name": "Azure/arm-ttk",
"url": "https://api.github.com/repos/Azure/arm-ttk"
},
"payload": {
"action": "opened",
"number": 804,
"pull_request": {
"url": "https://api.github.com/repos/Azure/arm-ttk/pulls/804",
"id": 4608504314,
"number": 804,
"head": {
"ref": "patch-9",
"sha": "b24dfebe858e303ea9d85fd42df2edab031be0ca",
"repo": {
"id": 1339873593,
"url": "https://api.github.com/repos/cyrillofrancisco30-lgtm/arm-ttk",
"name": "arm-ttk"
}
},
"base": {
"ref": "master",
"sha": "0ec9a41a4503e970a0ec8efb0cd08415cc172175",
"repo": {
"id": 221085904,
"url": "https://api.github.com/repos/Azure/arm-ttk",
"name": "arm-ttk"
}
}
}
},
"public": true,
"created_at": "2026-09-23T00:59:51Z",
"org": {
"id": 6844498,
"login": "Azure",
"gravatar_id": "",
"url": "https://api.github.com/orgs/Azure",
"avatar_url": "https://avatars.githubusercontent.com/u/6844498?"
}
},
{
"id": "21881370028",
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
"push_id": 44295680017,
"ref": "refs/heads/main",
"head": "f568c9d68ea145d87b80fa46f98ef1dc449b700a",
"before": "9ea8637e9216963bbe8750e0fde84bed7d604f3c"
},
"public": true,
"created_at": "2026-09-22T20:16:42Z"
},
{
"id": "21875130862",
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
"push_id": 44297241635,
"ref": "refs/heads/main",
"head": "b073a1a31b6815a12e384cb1a758938da0e34815",
"before": "f568c9d68ea145d87b80fa46f98ef1dc449b700a"
},
"public": true,
"created_at": "2026-09-22T20:38:00Z"
},
{
"id": "21869270744",
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
"push_id": 44294747033,
"ref": "refs/heads/main",
"head": "9ea8637e9216963bbe8750e0fde84bed7d604f3c",
"before": "4c8267399026dfc8c7c639a3753e7d5baca38f09"
},
"public": true,
"created_at": "2026-09-22T20:04:23Z"
},
{
"id": "21862778474",
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
"push_id": 44259050991,
"ref": "refs/heads/patch-7",
"head": "31c6e283216659502bcaee502b7abfdd4dcb7f01",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-09-22T12:50:56Z"
},
{
"id": "21857858899",
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
"push_id": 44269538197,
"ref": "refs/heads/patch-8",
"head": "41e2e005abd3026b8fcc0ca71b9781b407085cd9",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-09-22T14:50:02Z"
},
{
"id": "21839553045",
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
"push_id": 44258768724,
"ref": "refs/heads/patch-6",
"head": "6c4f7b55205b73dca9320847b8bc4d84baa635f8",
"before": "0ec9a41a4503e970a0ec8efb0cd08415cc172175"
},
"public": true,
"created_at": "2026-09-22T12:47:31Z"
}
]
