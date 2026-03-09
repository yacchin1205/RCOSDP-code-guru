# RCOSDP Code Guru
[![Launch Binder](https://binder.cs.rcos.nii.ac.jp/badge_logo.svg)](https://binder.cs.rcos.nii.ac.jp/v2/gh/yacchin1205/RCOSDP-code-guru/HEAD)

## 何ができるか
- RCOSDP Organization の公開リポジトリについて、Codex に質問できる。
- 大量リポジトリでも、必要なものだけ取得して回答できる。

## 使い方
[![Launch Binder](https://binder.cs.rcos.nii.ac.jp/badge_logo.svg)](https://binder.cs.rcos.nii.ac.jp/v2/gh/yacchin1205/RCOSDP-code-guru/HEAD)  をクリックして環境を起動する。

> [国立情報学研究所 データ解析機能](https://support.rdm.nii.ac.jp/usermanual/DataAnalysis-01/) を利用可能なアカウントを所有している必要があります。
> なお、 `mybinder.org` の使用は推奨しません。（`codex login` で保存されうる機微情報を扱う用途は想定されていないため）。

1. JupyterLab で `Terminal` を開く。
2. `codex login --device-auth` を実行してログインする。
3. `codex` を実行する。
4. 質問する。

## 開発者向け
### 前提
- 対象は公開情報のみ。
- private repository は扱わない。
- Binder 環境は一時的（セッション終了で消える）。

### 仕組み
1. Codex が `catalog/repos.jsonl` / `catalog/tree.jsonl` から候補リポジトリを絞る。
2. 必要なリポジトリだけ `workspace/repos/` に shallow clone する。
3. 該当箇所を調べて回答する。

### Catalog更新
Catalog は事前に生成しておく。 (リポジトリ管理者が実施)

```bash
python3 scripts/build_catalog.py --org RCOSDP --out-dir catalog --limit 500
```

生成物:
- `catalog/repos.jsonl`: 公開リポジトリのメタ情報
- `catalog/tree.jsonl`: 軽量ディレクトリ情報
- `catalog/bootstrap.md`: 要約情報
