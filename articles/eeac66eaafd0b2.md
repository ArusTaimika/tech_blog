---
title: "[DroidCam] スマートフォンをPCのWebカメラにする"
emoji: "🎃"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["obs", "camera", "webcam", "windows"]
published: false
---

## 🎯 概要

### 課題

- 解決したい課題：Windows PCに複数のカメラを接続し，異なる視点から撮影・録画したい．
- 導入前の問題点：
  - 高画質なWebカメラは購入費用が高い．
  - USB接続では，ケーブルの長さや配線が設置場所の制約になる．

### ✅ 結論

**DroidCamを使用すれば，スマートフォンをPCのWebカメラとして活用できる．**

OBSのプラグインを利用することで，OBS上でスマートフォンの映像を扱えるようになる．

- 使用ツール：DroidCam，OBS Studio
- 対象環境：Windows PC，AndroidまたはiOS端末

> 💡 DroidCam単体のソフトウェアも存在するが，PCのスペックに余裕がある場合，OBS使用者は，OBSプラグイン版の利用を推奨する．

## 💡 背景・目的

### 背景

実験の様子を複数の視点から撮影・録画する必要があった．しかし，Webカメラを複数台購入すると費用がかかり，USBケーブルによる接続では設置場所も制限される．

そこで，手持ちのスマートフォンをWebカメラとして利用する方法を検討した．

### 目的

- スマートフォンをカメラとして再利用し，機材の購入費用を抑える．
- 複数の視点から撮影・録画できる環境を構築する．
- Wi-Fi接続を活用し，USBケーブルによる設置場所の制約を減らす．

### 使用環境

| 項目 | 内容 |
|---|---|
| PC | Windows PC |
| カメラ | Androidスマートフォン，またはiPhone・iPad |
| 映像ソフトウェア | OBS Studio |
| 接続アプリ | DroidCam |

## 🛠️ 手順・苦戦ポイント

### 1. 導入・設定手順

#### Step 0. 通信環境の確認
1. スマートフォンとPCを同じWi-Fi環境下に設置する

#### Step 1. OBS Studioをインストールする

1. [OBS Studio公式サイト](https://obsproject.com/ja/download)を開く．
2. Windows版のインストーラーをダウンロードする．
3. インストーラーを実行し，OBS Studioをインストールする．
4. OBS Studioを起動し，正常に動作することを確認する．
5. 確認後，OBS Studioを終了する．
※ DroidCamのプラグインを適用するために，OBSを再起動する必要がある

#### Step 2. DroidCamのOBSプラグインをインストールする

1. [DroidCam公式サイト](https://droidcam.app/)を開く．
2. OBS用のDroidCamプラグインをダウンロードする．
3. ダウンロードしたファイルを実行し，インストールする．

#### Step 3. スマートフォンにDroidCamをインストールする

1. 使用するスマートフォンでDroidCamをインストールする．
2. DroidCamを起動する．
3. アプリに表示されるスマートフォンのIPアドレス(xxx.yyy.zzz.ttt)を控える
![phone](/images/articles/eeac66eaafd0b2_phone.png =400x)

#### Step 4. OBSからDroidCamを設定する

1. PCでOBS Studioを起動する．
2. ソースの追加画面を開き，DroidCamが追加されていることを確認する．
![OBS](/images/articles/eeac66eaafd0b2_obs.png =400x)
3. DroidCamを追加する．
4. 接続先のWi-Fi IP（xxx.yyyy.zzz.ttt）アドレスを入力する．ポートはデフォルトで"4747"
5. Activateをクリック
![droidcam](/images/articles/eeac66eaafd0b2_droidcam.png =400x)

#### Step 5. 動作確認

スマートフォンとOBSの接続が確立すると，スマートフォン側の画面が自動的に切り替わる．OBS上で映像が表示されることを確認する．

- [ ] OBS Studioが正常に起動する．
- [ ] DroidCamがOBSのソースとして追加できる．
- [ ] 接続先のIPアドレスを設定できる．
- [ ] スマートフォンとPCが接続される．
- [ ] OBS上にスマートフォンの映像が表示される．

### 2. 苦戦ポイント

#### ⚠️ 接続時の注意点

DroidCamの接続には，スマートフォンとPC間の通信設定が必要である．Wi-Fi接続では，接続先のIPアドレスを正しく指定する必要がある．


#### 🔍 確認事項

接続できない場合は，次の項目を確認するとよい．

1. PCとスマートフォンの両方でDroidCamの設定が完了しているか．
2. 入力したIPアドレスが正しいか．
3. ファイアウォールなどが通信を妨げていないか．
4. Activateをクリックし忘れていないか．

※ 上記は一般的な確認項目であり，実際に発生した問題や原因を示すものではない．

## 📝 まとめ

今回の記事では，DroidCamとOBS Studioを利用し，スマートフォンをPCのWebカメラとして活用する方法を整理した．

| 項目 | 内容 |
|---|---|
| 実現したいこと | スマートフォンをWebカメラとして利用する |
| 使用ツール | DroidCam，OBS Studio |
| 接続方法 | Wi-Fi，USBなど |
| 主なメリット | カメラの購入費用を抑え，撮影場所の自由度を高められる |
| 今後の課題 | 複数端末での同時接続や映像品質，遅延の検証 |

スマートフォンを再利用することで，Webカメラを新たに購入することなく，撮影環境を構築できる可能性がある．特に，実験や作業の様子を複数の視点から記録したい場合に有用である．

## 🔗 参考リンク

- [DroidCam公式サイト](https://droidcam.app/)
- [OBS Studio公式サイト](https://obsproject.com/ja/download)
