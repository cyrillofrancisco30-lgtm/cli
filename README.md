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

Conclusão: há evidência pública de uma contribuição documental concreta ao `Azure/arm-ttk`, com 148 linhas adicionadas e uma arquitetura de verificação de execução explicitamente descrita. Isso fortalece a evidência de contribuição e de especificação técnica; a execução real e a validação independente continuam sendo questões distintas que precisam ser verificadas.# GitHub CLI

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
