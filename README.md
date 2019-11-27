# 概要

* 今のところ  
https://os.phil-opp.com/  
の  
https://github.com/phil-opp/blog_os/tree/post-10  
の単なるコピー
* 一応コードはコピペではなく意味を理解した上で手打ちしているので、これくらいのRustならわかりますというのを示してはいる  
* そのうちブランチ切ってオリジナル機能足したりとかできるといいなあ（野望）  

# Usage

* macOS High Sierra(10.13.6)

* 以下、rustupが入ってる必要あり

* ビルドにはnightly toolchainが必要だが、rust-toolchainに書いてあるので下の`cargo install`などでcargoを触ると勝手に入る＆それを使うようになるはず。`rustup override set`とかしなくてよい。  
（明示的に入れるなら  
`rustup toolchain install nightly`  
）
* nightlyのバージョンは固定しない（やばいかも）。一応 `rustc 1.41.0-nightly (412f43ac5 2019-11-24)` を含むやつが、testが通ることを確認した最新のバージョン。
* ビルドにはcargo-xbuild, bootimageが必要。  
`cargo install cargo-xbuild bootimage`  
* `cargo xbuild`でビルド  
* なんかビルドしようとすると`rustup component add rust-src`しろとか言われるっぽい？やればok

* テストや実行にはqemu-system-x86_64(4.1.0)が必要
* `cargo xrun`でqemu実行  
`rustup component add llvm-tools-preview`しろと言われるかも、すればよい
* `cargo xtest`でテスト  

* 普通の`cargo test`や`cargo run`は通らないので注意  

# メモとか

* `cargo test`について、rustのtesting frameworkがstandart libraryに暗黙に依存してるってのもダメな理由の1つらしい
* rustup  
https://github.com/rust-lang/rustup  
release channel = stable, beta, nightly  
```
Standard release channel toolchain names have the following form:

<channel>[-<date>][-<host>]

<channel>       = stable|beta|nightly|<version>
<date>          = YYYY-MM-DD
<host>          = <target-triple>
```
* nightlyのリリース日固定したかったんだが、rust-toolchainの中にnightly+リリース日を書くとcargoがclippyというcomponentを要求してきて動かなくなる（cargoを使わないとclippy入れられないのに）ので困る　一応rust-toolchainに日付書かずにnightlyでclippy入れて後で日付書けばバージョン固定できそうな気がするけどそれを強要してもめんどいだけだろうと思ったのでやめた
