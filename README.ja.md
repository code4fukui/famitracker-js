# FamiTracker CX

> 開発が終了した、NES/Famicom向け音楽トラッカー「FamiTracker」のクロスプラットフォーム移植版です。

> **注意:** リポジトリ名は「famitracker-js」となっていますが、これはC++のプロジェクトです。この名前は歴史的な名残です。

> **プロジェクトステータス: 開発終了**
> 本プロジェクトは歴史的資料として保存されているアーカイブプロジェクトであり、現在はメンテナンスされていません。

FamiTracker CXは、人気の[FamiTracker](http://famitracker.com/)をフリーかつクロスプラットフォームにフォークしたもので、NES/Famicom向け音楽トラッカーをLinux環境へ導入することを目的に作成されました。コアコードはJonathan Liss (jsr) 氏のオリジナル版に基づいており、移植作業および新規コンポーネントの作成はDan Spencerが行いました。

## 機能

*   **クロスプラットフォームGUI:** オリジナルのWindowsベースのUIをQt 4ライブラリを用いてゼロから書き直し、Linux上でネイティブに動作するようにしました。
*   **複数のインターフェース:** フル機能のグラフィカルエディタ (Qt)、ターミナルベースのプレイヤー (ncurses)、およびシンプルなコマンドラインプレイヤーを搭載しています。
*   **Linuxオーディオサポート:** ALSAおよびJACKオーディオバックエンドをネイティブサポートしています。
*   **モジュラーアーキテクチャ:** オリジナルのコードベースを再利用可能なコンポーネントにリファクタリングし、複数のフロントエンドをサポートできるようにしました。
*   **拡張音源チップサポート:** VRC6、MMC5、FDS、VRC7など、さまざまなサウンドチップをエミュレートします。

## ソースからのビルド

### 依存関係
*   CMake
*   C++コンパイラ (例: g++)
*   Qt 4 開発ライブラリ
*   ALSA 開発ライブラリ (`libasound2-dev`)
*   JACK 開発ライブラリ (`libjack-dev`)
*   ncurses 開発ライブラリ (`libncurses5-dev`)
*   Boost Thread ライブラリ (`libboost-thread-dev`)

### ビルド手順
```bash
# リポジトリをクローン
git clone https://github.com/your-user/famitracker-js.git
cd famitracker-js

# ビルドを構成
cmake .

# プロジェクトをコンパイル
make
```

## 使用方法

ビルド後、同梱されているシェルスクリプトを使用して各インターフェースを実行できます。これらのスクリプトは適切なライブラリパスを自動的に設定します。

*   **Qt GUI:** `./src/qt-gui/install/famitracker-qt.sh`
*   **ncursesプレイヤー:** `./src/ncurses-ui/install/famitracker-nc.sh`
*   **コンソールプレイヤー:** `./src/console-play-ui/install/famitracker-play.sh`

## プロジェクトの事後分析

このセクションは、本プロジェクトにおける課題や得られた教訓に関する、移植者本人のメモをそのまま残したものです。

#### 課題
*   MFC/Win32のコードベースのQtへの移植。
*   複数のUIフロントエンドに対応するため、オリジナルコードを再利用可能なコンポーネントへモジュール化すること (オリジナル版ではすべての `.cpp` ファイルが単一のディレクトリに置かれていた)。
*   オリジナルコードに残存していた未定義動作 (Undefined Behavior) が、Linux版でバグを引き起こしたこと。

#### FamiTracker CXでのコーディングミス
*   「スレッドプール」が真のスレッドプールではなく、メッセージキューとして実装されていた。
*   `typedef` の代わりに、構造体に対して `type_t` 表記を使用してしまった。
*   Qt GUIのドキュメントデータの管理にグローバルな状態 (Global state) を使用してしまった。
*   サウンドシンクの実装で継承を乱用し、多くのオーディオ関連のバグを引き起こした。

#### もしこのプロジェクトをもう一度やり直すとしたら
オリジナル版の作者 (jsr) との緊密な連携が鍵になったでしょう。最初からコードベースを再利用できるように整理し、Gitのような分散型バージョン管理システム (DVCS) で開発ブランチを管理していれば、このフォークが直面した問題の多くは解決できたはずです。

## クレジットと帰属

*   **オリジナル版 FamiTracker:** Jonathan Liss (jsr) 氏およびその他の貢献者。プロジェクトページ: [http://famitracker.com/](http://famitracker.com/)
*   **FamiTracker CX 移植:** Dan Spencer (nukethepotato)
*   **アイコン:** Kuhneghetz
*   **ツールバーアイコン:** ilkke
*   **エクスポートプラグインサポート:** Gradualore
*   **DPCMインポートリサンプラー:** Jahrmander
*   **サードパーティライブラリ:**
    *   `blip_buffer` by blargg
    *   YM2413 & YM2149 エミュレータ by Mitsutaka Okazaki
    *   FDS サウンドエミュレータ from nezplug

## ライセンス

MIT License — 詳細は [LICENSE](LICENSE) を参照してください。
