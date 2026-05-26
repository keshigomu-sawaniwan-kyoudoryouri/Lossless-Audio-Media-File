*LAMF (Lossless Audio Media File)** - フォーマット専用CLIプレーヤー*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Windows](https://img.shields.io/badge/Windows-0078D6?logo=windows&logoColor=white)](https://www.microsoft.com/windows)

---

## 必ずREADMEをお読みください。自分のPCに合わせすぎてディレクトリのずれが生じています。

## 🎵 概要

LAMFは、個人用に設計した**無圧縮リニアPCMフォーマット**です。
CD品質（16bit/44.1kHz）からハイレゾ（24bit/48kHz）まで対応。

このリポジトリには、LAMFファイルを扱うための以下のツールが含まれます。

| ツール | 説明 |
|--------|------|
| `player.py` | CLI専用プレーヤー（ASCIIアート + プログレスバー + キー操作） |
| `convert.py` | WAV / FLAC / m4a(ALAC) ↔ LAMF 変換 |
| `ripping.py` | フォルダ監視 + 自動変換ウォッチャー（EAC連携） |
| `register.py` | Windows関連付けツール |

---

## 🚀 特徴

- 🎨 **クールなASCIIアート** - 起動時に表示されるかっこいいロゴ
- 📊 **プログレスバー** - インストーラー風の進行表示
- 🎹 **キー操作** - スペースで再生/一時停止、矢印でシーク/曲送り
- 📁 **フォルダプレイリスト** - EXE単体起動でフォルダ選択 → 全曲再生
- 🔄 **自動変換** - EACでリッピングしたWAV/FLAC/m4aを自動でLAMFに変換
- 🪟 **Windows関連付け** - `.lamf`ファイルをダブルクリックで再生

---

📋 キー操作

| キー | 動作 |
|------|------|
| `Space` | 再生 / 一時停止 |
| `→` | 5秒スキップ |
| `←` | 5秒巻き戻し |
| `↑` | 次の曲 |
| `↓` | 前の曲 |
| `q` | 終了 |

※ プレーヤーウィンドウがアクティブなときのみ操作可能です。

---

## 💻 インストール

### 必要なライブラリ

```bash
pip install -r requirements.txt
```

### EXE化（オプション）

```bash
py -m PyInstaller --onefile player.py --name LAMF_Player --hidden-import=keyboard
```

---

## 🔧 使い方

### プレーヤー

| 起動方法 | 動作 |
|----------|------|
| `.lamf`ファイルをダブルクリック | その1曲を再生 |
| `LAMF_Player.exe`を直接起動 | フォルダ選択ダイアログ → 全曲プレイリスト再生 |

### 変換

```bash
# WAV → LAMF
python convert.py input.wav

# FLAC → LAMF
python convert.py input.flac

# m4a(ALAC) → LAMF
python convert.py input.m4a

# LAMF → WAV
python convert.py input.lamf --to-wav
```

### 自動変換ウォッチャー

```bash
# 監視開始（D:/LAMFファイル変換 を監視）
python Converter.py

# EACなどリッピングソフトでリッピング先を D:/LAMFファイル変換 に設定すると、
# 自動で LAMF変換 → T:/music/CD_LAMF に保存 → 元ファイル削除
#EACでなくともWAV/FLAC/M4A(ALAC)で保存したファイルであればD:/LAMFファイル変換　より検知し変換が可能です。
```

## 📁 フォーマット仕様

| 項目 | 内容 |
|------|------|
| 拡張子 | `.lamf` |
| マジックナンバー | `LAMF` |
| 種別 | 無圧縮リニアPCM |
| サンプリングレート | 44.1kHz, 48kHz |
| ビット深度 | 16bit, 24bit |
| チャンネル | 1（モノラル）, 2（ステレオ） |
| エンディアン | リトルエンディアン |

詳細は [LAMF_SPEC.md](docs/LAMF_SPEC.md) 参照。

---

## 🗂️ ファイル構成

```
LAMF-Player/
├── convert.py          # WAV/FLAC/m4a ↔ LAMF変換
├── player.py           # メインプレーヤー
├── ripping.py          # 自動変換ウォッチャー
├── register.py         # Windows関連付け
├── requirements.txt
├── README.md
└── LAMF_SPEC.md
```

---

## 📜 ライセンス

[MIT License](LICENSE)

Copyright (c) 2025 jinhibi13-pixel

---

## 🙏 謝辞

- `sounddevice` / `numpy` - 音声再生エンジン
- `keyboard` - キー入力検知
- `ffmpeg` - FLAC/m4a変換
- Exact Audio Copy (EAC) - CDリッピング連携

---

**Made with 🖤 by jinhibi13-pixel**
