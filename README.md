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

### ローカルでテストを実行する

```bash
go test go/excellent/*.go
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
