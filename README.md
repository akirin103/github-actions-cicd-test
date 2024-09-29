# github-actions-cicd-test
Github Actionsを用いたCI/CDのテスト用リポジトリです。

## メモ

### Github CLIでリポジトリを作成する

```bash
gh repo create github-actions-cicd-test --public --clone --add-readme
```

### Github CLIからマニュアルトリガーでワークフローを実行する

```bash
gh workflow run manual.yml -f greeting="Hello from CLI"
```
