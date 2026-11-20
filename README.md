# Silent Comfort — VPM リポジトリ

Silent Comfort の VRChat ワールド向けギミックを、VCC / ALCOM から入れるための一覧（VPM Repo Listing）です。

## VCC / ALCOM に追加する

次の URL を、VCC / ALCOM の **Settings > Packages > Add Repository** に入れます。

```
https://silent-dandy.github.io/vpm/index.json
```

[https://silent-dandy.github.io/vpm/](https://silent-dandy.github.io/vpm/) の **Add to VCC** ボタンからも追加できます。

## このリポジトリの仕組み（管理用）

VRChat 公式の [template-package-listing](https://github.com/vrchat-community/template-package-listing) をもとにしています。

- `source.json` に書いたリポジトリの GitHub Releases を集めて、`index.json` とトップページを作る
- 作り直しは `.github/workflows/build-listing.yml`。`main` の `source.json` を変えたとき、または Actions から手動で実行したときに動く
- `Website/` はトップページのひな形。`source.json` の内容が自動で入る

### 最初に一度だけ

1. **Settings > Pages > Build and deployment** の Source を **GitHub Actions** にする
2. **Actions > Build Repo Listing > Run workflow** で作り直す
3. `https://silent-dandy.github.io/vpm/index.json` が開けることを確かめる

### パッケージを足す

1. パッケージのリポジトリ（例：`silent-dandy/WorldNadenade`）を公開にし、template-package の Build Release で、zip を添付したリリースを作る
2. `source.json` の `githubRepos` にそのリポジトリを足す

```json
"githubRepos": [
    "silent-dandy/WorldNadenade"
]
```

3. `main` に入れると一覧が作り直される

### 新しい版を出したとき

パッケージ側でリリースを作ったあと、**Actions > Build Repo Listing > Run workflow** で作り直します（`source.json` を変えないときは自動では動きません）。

### 変えてはいけないもの

`source.json` の `url` と `id` は、利用者の VCC に登録されます。公開後に変えると更新が届かなくなるので、変えないでください。
