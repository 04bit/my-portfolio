





# MEMO
npm に npm-chack-update をインストールした。自動的にバージョンを更新してくれる。
```
npm install -g npm-check-updates
ncu
ncu -u
```



## ERROR

### npm start
```
PS C:\Users\username\my-portfolio> npm start

> my-portfolio@0.1.0 start
> react-scripts start

Could not find a required file.
  Name: index.js
  Searched in: C:\Users\username\my-portfolio\src
  ```
#### 解決策

今回は React を用いる為 index.js は不要。index.tsx を作成する。
- index.tsx を src フォルダに作成する(main.tsx の場合、index.tsx にリネームする) 
- public/index.html に、```<div id="root"></div>```があることを確認する


***

### react-scripts version error
react-scripts と typescript には依存関係があり、それによって脆弱性が変化する。エラーの発生原因は、バージョンの不一致。 
```pwsh
# npm audit report

nth-check  <2.0.1
Severity: high
Inefficient Regular Expression Complexity in nth-check - https://github.com/advisories/GHSA-rp65-9cf3-cjxr
fix available via `npm audit fix --force`
Will install react-scripts@3.0.1, which is a breaking change
node_modules/react-scripts/node_modules/nth-check
  css-select  <=3.1.0
  Depends on vulnerable versions of nth-check
  node_modules/react-scripts/node_modules/css-select
    svgo  1.0.0 - 1.3.2
    Depends on vulnerable versions of css-select
    node_modules/react-scripts/node_modules/svgo
      @svgr/plugin-svgo  <=5.5.0
      Depends on vulnerable versions of svgo
      node_modules/react-scripts/node_modules/@svgr/plugin-svgo
        @svgr/webpack  4.0.0 - 5.5.0
        Depends on vulnerable versions of @svgr/plugin-svgo
        node_modules/react-scripts/node_modules/@svgr/webpack
          react-scripts  >=2.1.4
          Depends on vulnerable versions of @svgr/webpack
          Depends on vulnerable versions of resolve-url-loader
          node_modules/react-scripts

postcss  <8.4.31
Severity: moderate
PostCSS line return parsing error - https://github.com/advisories/GHSA-7fh5-64p2-3v2j
fix available via `npm audit fix --force`
Will install react-scripts@3.0.1, which is a breaking change
node_modules/resolve-url-loader/node_modules/postcss
  resolve-url-loader  0.0.1-experiment-postcss || 3.0.0-alpha.1 - 4.0.0
  Depends on vulnerable versions of postcss
  node_modules/resolve-url-loader

8 vulnerabilities (2 moderate, 6 high)

To address all issues (including breaking changes), run:
  npm audit fix --force
```
#### 対策
当初は、126件脆弱性が現れていた。react-scripts@5.0.1 によって、8件まで減少した。

npm audit で依存関係とエラーを確認することができる。

