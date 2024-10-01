# github-actions-cicd-test
Github Actionsを用いたCI/CDのテスト用リポジトリです。  
書籍「GitHub CI/CD実践ガイド――持続可能なソフトウェア開発を支えるGitHub Actionsの設計と運用」の内容を参考にしています。

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
