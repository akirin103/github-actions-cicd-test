# github-actions-cicd-test
Github Actionsを用いたCI/CDのテスト用リポジトリです。  
書籍「GitHub CI/CD実践ガイド――持続可能なソフトウェア開発を支えるGitHub Actionsの設計と運用」の内容を参考にしています。  
なお、Github Actionsのプランの関係で、一時的にパブリックリポジトリに配置しています。

## メモ

### Github CLIでリポジトリを作成する

```bash
gh repo create github-actions-cicd-test --public --clone --add-readme
```

### Github CLIからマニュアルトリガーでワークフローを実行する

```bash
gh workflow run manual.yml -f greeting="Hello from CLI"
```

### actionlintでワークフローの構文をチェックする

```bash
docker run --rm -v "$(pwd):$(pwd)" -w "$(pwd)" rhysd/actionlint:latest
```

### ワークフロー中に使用するshellについて
shellの指定がないと、パイプエラーが拾えないため、ワークフローのデフォルトでbashを指定しておくと良い。(pipefailを有効にするため)

```yaml
defaults:
  run:
    shell: bash
```

### Github Releasesの作成
Gitタグの作成とリリースノードの作成を同時に行う。

```bash
gh release create v1.0.0 --title "v1.0.0" --notes "Release v1.0.0" --target main
# ノートを自動生成する場合
gh release create v2.1.0 --title "v2.1.0" --generate-notes
```

### Github CLIでプルリクエストを作成、マージする(カレントブランチをベース)

```bash
gh pr create --fill-first --label "enhancement"
gh pr merge --merge
```

## メモ(go言語関連)
### ローカルでテストを実行する

```bash
go test go/excellent/*.go
```

### ローカルでビルド時にバージョン情報を埋め込む

```bash
go build -o example -ldflags "-X main.version=v2.2.0" go/example/main.go
```

## Github Packages(Github Container Registry)にイメージをプッシュする

```bash
export GHCR_USER=$(gh config get -h github.com user)

docker build -t ghcr.io/${GHCR_USER}/example:latest docker/example

# Github Packagesへの権限追加
gh auth refresh --scopes write:packages

# Github Packagesへのログイン
gh auth token | docker login ghcr.io -u $GHCR_USER --password-stdin

docker push ghcr.io/${GHCR_USER}/example:latest
```
