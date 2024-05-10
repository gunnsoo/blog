---
title: "MacBook Air (M1, 2020) セットアップ"
date: 2021-09-11T10:18:05+09:00
draft: false
tags: [ "PC" ]
---

M1 MacBook Air 買いました。

MacBook Proの2017年モデルをずっと使っていたのですが、動きがもっさりしてきたので買い替えました。

充電のもちとサクサクさに驚いてます。めっちゃ快適。

備忘録として最初にした設定をまとめておきます。

\
&nbsp;
### Mac本体
* * *
**タップを有効化**  
設定->トラックパッド->タップでクリック

**カーソルを速くする**  
設定->トラックパッド->軌跡の速さ

**CapsLockをControlに**  
設定->キーボード->修飾キー

\
&nbsp;
### Terminal
* * *
iTerm2を入れます。

iTerm2は前から使っており、Macを買い替えたのを機に変えようかとも思って色々検討したのですが、結局iTerm2に落ち着きました。

色々検討するにあたってはこの記事が参考になりました。  
https://zenn.dev/kawarimidoll/articles/007449407cc78d

Hyperでデザインおしゃれにしたり、Alacrittyはなんかクールな雰囲気なので、使ってみたかったのですが今回は断念。いつか乗り換えるかも。

**hotkeyを有効に**  
参考記事
https://qiita.com/ruwatana/items/8d9c174250061721ad11

**Material Themeを適用**  
https://github.com/MartinSeeler/iterm2-material-design

**StarShipを入れる**  
プロンプトをおしゃれにしてくれるStarShipを入れます。  
https://starship.rs/

いろんなシェルに対応してるので移行も簡単。

前準備としてNerd Fontをインストールする必要があります。

筆者はFira Codeにしました。  
https://github.com/tonsky/FiraCode

\
&nbsp;
### Editor
* * *
VSCodeを入れます。

**codeコマンド**  
codeコマンドのpathを通します。  
https://code.visualstudio.com/docs/setup/mac

#**Material ThemeとMaterial Theme Iconsを適用**  
https://github.com/material-theme

**フォントをFira Codeに**  
Fira Codeが見やすいので、デフォルトのフォントから変更します。  
https://wonwon-eater.com/fira-code/

\
&nbsp;
### Apps
* * *
便利なアプリを入れていきます。

**Chrome**  
みんな大好き？Chromeを入れてデフォルトブラウザーに設定。

**RunCat**  
メニューバーでネコを飼える。癒されます。
https://qiita.com/Kyome/items/b85e7cfc2716a6f880ee

**Clippy**  
コピペ多用人間には必須。  
https://qiita.com/iwaseasahi/items/023964b426305375489e

\
&nbsp;
### dotfiles
* * *
もろもろの設定を管理するレポジトリを作る。  
https://github.com/gunnsoo/dotfiles

\
&nbsp;