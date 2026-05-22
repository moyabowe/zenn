---
title: "はじめての完全自作キーボード（0.構想・選定）"
emoji: "👌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["自作キーボード"]
published: false
---
GW初日、ふと思いました。
「そうだ、オリジナルキーボード作ろう。」

自作キーボードキットを組み立てたことはありますが、
基板から自作するのは初めてです。

## 構想
未経験で「フルサイズ両手分割キーボード」を作るのは厳そうなので、
キー数の少ない、実験用キーパッドにしようと思います。

- **自キでよくあるパーツをたくさん搭載**（ファームウェア作成の練習のため）
  - OLED
  - ロータリーエンコーダ
  - RGBLED（バックライト、アンダーグロー）
  - 単色LED（NumLockなどのインジケータ用）
  - TRRSジャック
- **マトリックス配置のキー搭載**
  - キー数は6くらい
  - 6キー程度であればマトリックス配置は不要だが、後学のため
  - ホットスワップ対応
- **今回はケースやプレートは無し**
  - 後で作ろうと思えば作れるし
  - 代わりにスペーサーを足として付ける

## 部品選定
- なるべく遊舎工房、秋月電子で揃うよう選定
- チップ部品は1608サイズで統一（手はんだ可能な最小サイズ）
- ロータリーエンコーダにはフィルタ回路をつける
  - 10kΩ抵抗x4、0.01μFコンデンサx2
  - 回路図：https://tech.alpsalpine.com/j/products/detail/EC12E2440301/

## 部品リスト（BOM）
| 品名 | 型番 | 備考 | 商品ページ |
| ---- | ---- | ---- | --- |
| MCU | Pro Micro | Type-B | [リンク](https://shop.yushakobo.jp/products/pro-micro?_pos=3&_sid=65f2fbbec) |
| OLED | - | ピンソケット高さ合うかな？ | [リンク](https://shop.yushakobo.jp/products/oled?_pos=3&_sid=48f8f6a72&_ss=r) |
| ロータリーエンコーダ | - | EC12互換品 | [リンク](https://shop.yushakobo.jp/products/3762?_pos=2&_sid=c323c86df&_ss=r) |
| RGBLED | SK6812MINI-E | バックライト、アンダーグロー共通 | [リンク](https://shop.yushakobo.jp/products/sk6812mini-e-10?_pos=2&_sid=0f92a7f16&_ss=r) |
| 単色LED | - | 3mm砲弾型赤色LED | [リンク](https://akizukidenshi.com/catalog/g/g111577/) |
| TRRSジャック | - |  | [リンク](https://shop.yushakobo.jp/products/a0800tr-01-1?_pos=1&_sid=72b5fe88e&_ss=r) |
| スイッチソケット | - | Kailh Switch Socket | [リンク](https://shop.yushakobo.jp/products/a01ps?_pos=21&_sid=dbd7cb00f&_ss=r) |
| 抵抗（単色LED用） | - | チップ抵抗 1608 1/8W470Ω ※1 | [リンク](https://akizukidenshi.com/catalog/g/g130349/) |
| 抵抗（プルアップ用） | - | チップ抵抗 1608 1/10W4.7kΩ ※2 | [リンク](https://akizukidenshi.com/catalog/g/g130353/) |
| 抵抗（フィルタ回路用） | - | チップ抵抗 1608 1/10W10kΩ | [リンク](https://akizukidenshi.com/catalog/g/g130355/) |
| ダイオード | 1N4148W |  | [リンク](https://shop.yushakobo.jp/products/a0800di-02-100?_pos=2&_sid=08ce7537d&_ss=r) |
| コンデンサー | - | 0.01μF50V B 1608 | [リンク](https://akizukidenshi.com/catalog/g/g113387/) |

※1　抵抗値は VCC=5V、VF=2.1V、IF=20mA で計算（145Ω、0.058W）
※2　抵抗値は [QMK Docs](https://docs.qmk.fm/features/split_keyboard#hardware-configuration) に記載あり