# Antigravity Devcontainer with Path Workaround

このリポジトリは、**3つの要素**を統合した Antigravity devcontainer テンプレートです：

1. **Antigravity devcontainer 対応** - Antigravity (Google AI Studio) での devcontainer 開発に最適化
2. **Node.js & Python 環境** - Node.js 24 と Python 3.14.3（uv パッケージマネージャー付き）がプリインストール
3. **Path Workaround 統合** - [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround) の Antigravity パス互換性解決策を統合

---

This is an Antigravity devcontainer template integrating **3 key components**:

1. **Antigravity devcontainer support** - Optimized for devcontainer development in Antigravity (Google AI Studio)
2. **Node.js & Python environments** - Pre-installed Node.js 24 and Python 3.14.3 with uv package manager
3. **Path workaround integration** - Includes the Antigravity path compatibility solution from [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround)

---

## Template Repository Usage / テンプレートリポジトリの使い方

### English

#### How to Use as a Template Repository

1. **Create a New Repository from This Template**
   - Click the "Use this template" button on GitHub to create a new repository
   - Or use: `gh repo create --template mmurasawa/antigravity-devcontainer-template`

2. **Clone the New Repository**
   ```bash
   git clone <your-new-repo-url>
   cd <your-new-repo>
   ```

3. **Open in Antigravity (Google AI Studio)**
   - Open the cloned repository in Antigravity
   - The devcontainer starts automatically based on `.devcontainer/devcontainer.json` configuration

#### Expected State

- **Auto-Execution**: The `antigravity_path_watcher.sh` script runs automatically when the devcontainer starts
- **Symlink Creation**: Monitors `/home/vscode/.antigravity-server/bin` directory and creates symlinks for versioned binary paths
- **Path Issue Resolved**: Antigravity Remote Server's hash-based path references work correctly
- **Development Environment Ready**: You're ready to start development with Node.js environment as normal

### 日本語

#### テンプレートリポジトリとしての使い方

1. **このテンプレートから新しいリポジトリを作成**
   - GitHub で「Use this template」ボタンをクリックして、新しいリポジトリを作成します
   - または `gh repo create --template mmurasawa/antigravity-devcontainer-template` で作成

2. **新しいリポジトリをクローン**
   ```bash
   git clone <your-new-repo-url>
   cd <your-new-repo>
   ```

3. **Antigravity（Google AI Studio）で開く**
   - クローンしたリポジトリを Antigravity で開きます
   - `.devcontainer/devcontainer.json` 設定に基づいて自動的に devcontainer が起動します

#### 期待される状態

- **自動実行**: Devcontainer 起動時に `antigravity_path_watcher.sh` スクリプトが自動的に実行されます
- **シンボリックリンク作成**: `/home/vscode/.antigravity-server/bin` ディレクトリを監視し、バージョン付きパスのシンボリックリンクを作成
- **パス問題を解決**: Antigravity Remote Server のハッシュベースパス参照が正常に動作するようになります
- **開発環境準備完了**: Node.js 環境で通常通り開発を開始できる状態になります

## About This Template / このテンプレートについて

### English

This template is based on [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround), which provides a ready-to-use solution for the Antigravity Remote Server path compatibility issue in devcontainers.

The original repository contains the complete workaround implementation that has been tested and verified. This template repository repackages it for easy use with GitHub's "Use this template" feature, allowing developers to quickly set up new projects with the path workaround already configured.

### 日本語

このテンプレートは [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround) を基に作成されており、devcontainer での Antigravity Remote Server パス互換性の問題に対する実証済みのソリューションを提供します。

元のリポジトリには完全な実装が含まれています。このテンプレートリポジトリは、GitHub の「Use this template」機能で簡単に利用できる形に再パッケージ化しており、開発者が path workaround をすでに設定した状態で新しいプロジェクトをすぐに開始できます。

---

## Element 1: Antigravity Devcontainer Support / 要素1：Antigravity Devcontainer 対応

### The Problem / 問題

Antigravity (Google AI Studio) has a known issue with devcontainer binary path resolution:

```
Editor sends:        /home/vscode/.antigravity-server/bin/[HASH]/node
Actual path in container: /home/vscode/.antigravity-server/bin/[VERSION]-[HASH]/node
```

Antigravity には devcontainer のバイナリパス解決に関する既知の問題があります：

```
エディターが送信: /home/vscode/.antigravity-server/bin/[HASH]/node
コンテナ内の実際のパス: /home/vscode/.antigravity-server/bin/[VERSION]-[HASH]/node
```

### The Solution / ソリューション

This template includes an automated script (`antigravity_path_watcher.sh`) that monitors the binary directory and creates symlinks to handle versioned paths transparently.

このテンプレートに含まれる自動化スクリプト（`antigravity_path_watcher.sh`）が、バイナリディレクトリを監視し、バージョン付きパスをシンボリックリンクで透過的に処理します。

**How it works / 動作方法:**

1. **Monitoring / 監視**: Continuously watches `/home/vscode/.antigravity-server/bin` directory
2. **Pattern Matching / パターン認識**: Identifies `[VERSION]-[HASH]` pattern directories
3. **Symlink Creation / シンボリックリンク作成**: Creates hash-based symlinks automatically  
4. **Auto-Execution / 自動実行**: Runs when the devcontainer starts

**Reference / 参考**: [Antigravity Discuss Thread](https://discuss.ai.google.dev/t/root-cause-identified-temporary-workaround-to-users-and-google-developers-struggling-with-devcontainer-connection-issues/121549)

---

## Element 2: Node.js & Python Environments / 要素2：Node.js & Python 環境

### English

Pre-installed development environments ready for immediate use:

- **Node.js 24**: JavaScript/TypeScript runtime (installed via nvm)
- **Python 3.14.3**: Python runtime (installed via uv)
- **uv**: Ultra-fast Python package installer and resolver by Astral
- **Git**: Version control
- **OpenSSH Client**: Secure shell connectivity

Start developing JavaScript/TypeScript or Python projects without additional environment setup.

### 日本語

すぐに使用できる事前設定済みの開発環境：

- **Node.js 24**: JavaScript/TypeScript ランタイム（nvm 経由でインストール）
- **Python 3.14.3**: Python ランタイム（uv 経由でインストール）
- **uv**: Astral による高速 Python パッケージインストーラーとリソルバー
- **Git**: バージョン管理
- **OpenSSH Client**: セキュアシェル接続

追加の環境セットアップなしに、JavaScript/TypeScript または Python プロジェクトの開発をすぐに開始できます。

---

## Element 3: Path Workaround Integration / 要素3：Path Workaround 統合

### English

The third element is the integration of the proven path workaround from [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround). This workaround automatically handles the Antigravity binary path compatibility issue described in Element 1.

The `antigravity_path_watcher.sh` script runs automatically when your devcontainer starts, ensuring seamless path resolution without manual intervention.

### 日本語

3番目の要素は、[antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround) の実証済みの path workaround の統合です。この回避策は、要素1で説明した Antigravity バイナリパス互換性の問題を自動的に処理します。

`antigravity_path_watcher.sh` スクリプトは devcontainer 起動時に自動的に実行され、手動操作なしにシームレスなパス解決を実現します。

---

## Project Structure / プロジェクト構成

```
.devcontainer/
├── Dockerfile               # Devcontainer image definition
├── devcontainer.json        # VS Code devcontainer configuration
├── docker-compose.yml       # Docker Compose configuration
└── antigravity_path_watcher.sh  # Path workaround script
```

**Key Files:**

- **Dockerfile**: Defines the devcontainer environment with Node.js, Python, and uv
- **devcontainer.json**: VS Code configuration with Antigravity settings
- **docker-compose.yml**: Multi-service setup for devcontainer
- **antigravity_path_watcher.sh**: Core workaround script (automatically executed)

---

## Related Resources / 関連リソース

- **Original Repository**: [antigravity-devcontainer-with-pathworkaround](https://github.com/mmurasawa/antigravity-devcontainer-with-pathworkaround)
- **Antigravity Discussion**: [Root cause identified - Temporary workaround](https://discuss.ai.google.dev/t/root-cause-identified-temporary-workaround-to-users-and-google-developers-struggling-with-devcontainer-connection-issues/121549)
- **VS Code Devcontainers**: [Remote - Containers Documentation](https://code.visualstudio.com/docs/devcontainers/containers)

