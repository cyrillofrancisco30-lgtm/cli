#!/usr/bin/env python3
"""
JCS Evidence Producer for XA-TRUST / ECM (RFC 8785 Conformance)
Generates formal evidence artifacts for independent verification.
"""

import json
import sys
import os
import hashlib
import base64
from datetime import datetime
import subprocess

try:
    import rfc8785
except ImportError:
    print("[ERROR] Required library 'rfc8785' not found. Install via pip install rfc8785", file=sys.stderr)
    sys.exit(1)

# Configurações de Versão e Baseline
EXECUTOR_VERSION = "1.0.0"
VECTORS_PATH = "tests/jcs/vectors.json"

def get_sha256(data):
    if isinstance(data, str):
        data = data.encode('utf-8')
    return hashlib.sha256(data).hexdigest()

def get_git_head():
    try:
        return subprocess.check_output(['git', 'rev-parse', 'HEAD']).decode('utf-8').strip()
    except Exception:
        return "UNKNOWN_COMMIT"

def produce_evidence():
    if not os.path.exists(VECTORS_PATH):
        print(f"[ERROR] Vectors file not found at: {VECTORS_PATH}", file=sys.stderr)
        sys.exit(1)

    with open(VECTORS_PATH, "r", encoding="utf-8") as f:
        data = json.load(f)

    suite_name = data.get("suite", "Unknown Suite")
    vectors = data.get("vectors", [])
    
    print(f"=== Producing Evidence for {suite_name} ===")
    
    # 1. Gerar execution_metadata.json
    metadata = {
        "repository": "azhpc-extensions",
        "head_sha": get_git_head(),
        "workflow_run_id": os.environ.get("GITHUB_RUN_ID", "LOCAL_EXECUTION"),
        "timestamp": datetime.utcnow().isoformat() + "Z",
        "executor_version": EXECUTOR_VERSION,
        "environment": {
            "python_version": sys.version.split()[0],
            "rfc8785_version": "installed"
        }
    }
    
    # 2. Gerar artifact_hashes.json
    # Mapeia os arquivos que compõem a base de confiança da execução
    critical_files = [VECTORS_PATH]
    artifacts = []
    for path in critical_files:
        with open(path, "rb") as f:
            content = f.read()
            artifacts.append({
                "path": path,
                "sha256": hashlib.sha256(content).hexdigest(),
                "size_bytes": len(content)
            })
    
    # 3. Gerar test_execution.json (A evidência central)
    execution_results = []
    all_passed = True

    for vec in vectors:
        vid = vec.get("id")
        raw_input = vec.get("input")
        expected_canonical = vec.get("expected_canonical")

        try:
            # Produção de bytes JCS
            actual_bytes = rfc8785.dumps(raw_input)
            actual_bytes_b64 = base64.b64encode(actual_bytes).decode('utf-8')
            
            # Cálculos de Hash para a evidência
            # O input é serializado para hash para garantir determinismo da entrada
            input_json_bytes = json.dumps(raw_input, sort_keys=True).encode('utf-8')
            
            res_status = "PASS" if actual_bytes == expected_canonical.encode('utf-8') else "FAIL"
            if res_status == "FAIL":
                all_passed = False

            execution_results.append({
                "vector_id": vid,
                "input_sha256": get_sha256(input_json_bytes),
                "expected_sha256": get_sha256(expected_canonical),
                "actual_sha256": get_sha256(actual_bytes),
                "actual_bytes_base64": actual_bytes_b64,
                "result": res_status
            })
            print(f"[{res_status}] {vid}")

        except Exception as e:
            print(f"[ERROR] {vid}: {e}")
            execution_results.append({
                "vector_id": vid,
                "input_sha256": "ERROR",
                "expected_sha256": "ERROR",
                "actual_sha256": "ERROR",
                "actual_bytes_base64": "",
                "result": "ERROR"
            })
            all_passed = False

    # Persistência dos artefatos no disco
    with open("execution_metadata.json", "w") as f:
        json.dump(metadata, f, indent=2)
    
    with open("artifact_hashes.json", "w") as f:
        json.dump({"artifacts": artifacts}, f, indent=2)
        
    with open("test_execution.json", "w") as f:
        json.dump({"suite": suite_name, "results": execution_results}, f, indent=2)

    print("\n=== Evidence Production Complete ===")
    print("Artifacts generated: execution_metadata.json, artifact_hashes.json, test_execution.json")
    
    return all_passed

if __name__ == "__main__":
    success = produce_evidence()
    sys.exit(0 if success else 1)


# GitHub CLI

`gh` is GitHub on the command line. It brings pull requests, issues, and other GitHub concepts to the terminal next to where you are already working with `git` and your code.

![screenshot of gh pr status](https://user-images.githubusercontent.com/98482/84171218-327e7a80-aa40-11ea-8cd1-5177fc2d0e72.png)

GitHub CLI is available for repositories hosted on GitHub.com and GitHub Enterprise Server 2.20+, and to install on macOS, Windows, and Linux.

## Documentation

[See the manual][manual] for setup and usage instructions.

## Contributing

If anything feels off, or if you feel that some functionality is missing, please check out the [contributing page][contributing]. There you will find instructions for sharing your feedback, building the tool locally, and submitting pull requests to the project.


<!-- this anchor is linked to from elsewhere, so avoid renaming it -->
## Installation

### macOS

`gh` is available via [Homebrew][], [MacPorts][], and as a downloadable binary from the [releases page][].

#### Homebrew

| Install:          | Upgrade:          |
| ----------------- | ----------------- |
| `brew install gh` | `brew upgrade gh` |

#### MacPorts

| Install:               | Upgrade:                                       |
| ---------------------- | ---------------------------------------------- |
| `sudo port install gh` | `sudo port selfupdate && sudo port upgrade gh` |

### Linux

`gh` is available via [Homebrew](#homebrew), and as downloadable binaries from the [releases page][].

For more information and distro-specific instructions, see the [Linux installation docs](./docs/install_linux.md).

### Windows

`gh` is available via [WinGet][], [scoop][], [Chocolatey][], and as downloadable MSI.


#### WinGet

| Install:            | Upgrade:            |
| ------------------- | --------------------|
| `winget install gh` | `winget install gh` |

<i>WinGet does not have a specialized `upgrade` command yet, but the `install` command should work for upgrading to a newer version of GitHub CLI.</i>

#### scoop

| Install:           | Upgrade:           |
| ------------------ | ------------------ |
| `scoop install gh` | `scoop update gh`  |

#### Chocolatey

| Install:           | Upgrade:           |
| ------------------ | ------------------ |
| `choco install gh` | `choco upgrade gh` |

#### Signed MSI

MSI installers are available for download on the [releases page][].

### Other platforms

Download packaged binaries from the [releases page][].

### Build from source

See here on how to [build GitHub CLI from source][build from source].

## Comparison with hub

For many years, [hub][] was the unofficial GitHub CLI tool. `gh` is a new project that helps us explore
what an official GitHub CLI tool can look like with a fundamentally different design. While both
tools bring GitHub to the terminal, `hub` behaves as a proxy to `git`, and `gh` is a standalone
tool. Check out our [more detailed explanation][gh-vs-hub] to learn more.


[manual]: https://cli.github.com/manual/
[Homebrew]: https://brew.sh
[MacPorts]: https://www.macports.org
[winget]: https://github.com/microsoft/winget-cli
[scoop]: https://scoop.sh
[Chocolatey]: https://chocolatey.org
[releases page]: https://github.com/cli/cli/releases/latest
[hub]: https://github.com/github/hub
[contributing]: ./.github/CONTRIBUTING.md
[gh-vs-hub]: ./docs/gh-vs-hub.md
[build from source]: ./docs/source.md
