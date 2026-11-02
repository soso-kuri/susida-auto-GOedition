[README.md](https://github.com/user-attachments/files/34264210/README.md)
# OCR Auto Typer — Go Edition

**Windows向けOCR自動入力アプリ / OCR-based Auto Typing Utility for Windows**  
**Version: v1.0.2** | **Distribution: Installer only / インストーラーのみ配布**

[日本語](#日本語) | [English](#english)

> [!IMPORTANT]
> このリポジトリでは **Windows用インストーラー（Setup.exe）のみ**を配布します。Goのソースコードやビルド用ファイルは公開していません。  
> This repository distributes the **compiled Windows installer only**. Go source code and build tools are not included.

> [!WARNING]
> **ご利用前に必ずこのREADMEをお読みください。**  
> 寿司打の公式サイトは、外部ツールを用いた不正なタイピングやタイピング練習以外のテスト・実験を禁止しています。本アプリは非公式であり、寿司打・Neutralとは無関係です。利用規約で自動操作が禁止されているサービスには使用せず、許可されたテスト環境などでのみご利用ください。  
> **Please read this README before use.** The official Sushi-Da service prohibits improper automated typing with external tools and testing outside regular typing practice. This is an independent, unofficial project. Use it only in environments where automation is permitted.  
> [Neutralの利用条件 / Official usage rules](https://keyx0.net/about.html)

---

## 日本語

### 概要

**OCR Auto Typer — Go Edition v1.0.2** は、画面上で指定した1行のローマ字を **Tesseract OCR** で読み取り、Windowsのキーボード入力として自動送信するアプリです。Go言語とWindows APIを利用しています。

**主な機能**

- マウスでOCR認識範囲を選択
- 読み取った文字の確認とプレビュー画像保存
- 自動入力の開始・停止
- 「安定」「高速」「超高速」の3段階の速度切替
- `!`・`?` の入力対応と、末尾の `i` の認識・入力漏れ軽減（v1.0.2で調整）
- OCRが5回連続で失敗した場合の自動停止
- 日本語の操作画面、専用の **GO Edition** アイコン
- スタートメニューへの登録、任意のデスクトップショートカット、アンインストール対応

### 動作環境

- Windows 10 / 11（**64bit**）向け
- Windows用Setup.exeに、Goの実行に必要なコードとTesseract OCRを同梱する設計です
- **Python、Go SDK、.NET SDKのインストールは不要**です
- すべてのPC・画面構成で動作することを保証するものではありません

### ダウンロード・インストール

1. このリポジトリの **Releases** ページを開きます。
2. **v1.0.2** の **Assets** から `OCR-Auto-Typer-Go-Setup-1.0.2.exe` をダウンロードします。
3. ファイルの配布元を確認してから、Setup.exeを実行します。
4. セットアップの案内に従ってインストールします。デスクトップショートカットの作成は任意です。
5. Windowsのスタートメニューから **OCR Auto Typer - Go Edition** を起動します。

> **注意：** **Code → Download ZIP** ではインストーラーはダウンロードできません。**Releases → Assets** を利用してください。未署名のSetup.exeでは、Windows SmartScreenなどが警告を表示する場合があります。安全性を確認できないファイルは実行しないでください。

### 使い方

1. **自分が自動操作する許可を持つ**ローカルのテストページなどで、ローマ字を1行表示します。
2. アプリの **F6** または「範囲選択」ボタンで、文字列全体をドラッグして囲みます。末尾の `i` も余裕を持って含めてください。
3. 必要に応じて **F7** でOCRの認識結果を確認します。
4. 入力先のウィンドウ・入力欄をクリックし、IMEを半角英数入力にします。
5. **F8** で自動入力を開始し、**F9** で停止します。

| キー | 操作 |
| --- | --- |
| `F6` | OCR認識範囲を選択（選択中はEscでキャンセル） |
| `F7` | OCR結果を確認し、プレビュー画像を保存 |
| `F8` | 自動入力を開始・再開 |
| `F9` | 自動入力を停止 |
| `F10` | 速度切替：高速 → 超高速 → 安定 → 高速 |
| `Ctrl + Shift + Q` | アプリを終了 |

### v1.0.2の改善

- 通常の文字の入力速度は維持し、`i` の押下時間だけを少し延長
- 単語末尾の `i` に対するOCRの確認を強化
- v1.0.1のTesseract起動時に黒いコマンド画面が出る問題への修正を維持

> OCRの認識や入力の成功率が100%になるわけではありません。誤認識によって文字が抜けたり、余計な文字が送信されたりする可能性があります。

### よくある問題

| 症状 | 対処 |
| --- | --- |
| 文字を認識しない | F6でローマ字1行全体を選択し、F7で認識結果を確認 |
| 自動入力されない | 入力対象をクリックしてフォーカスを合わせ、IMEを半角英数にする |
| `i` の入力が抜ける | F10で「安定」モードを試し、選択範囲の右端に余裕を持たせる |
| `l` や `1` を誤認識する | OCRに `i` への簡易補正があり、一般英語の認識には不向きな場合がある |
| OCRが連続で失敗する | F7で認識画像を確認。インストール内のTesseract関連ファイルが揃っているか確認 |
| F6〜F10が反応しない | 他ソフトのショートカットとの競合を確認。画面内のボタンも利用可能 |
| 別のモニターで範囲選択できない | 現バージョンの範囲選択は主にプライマリモニターを対象とする |

**プレビュー画像について：** OCR確認で保存される `ocr_preview.png` は、通常 `%LOCALAPPDATA%\OCR-Auto-Typer-Go\` 内に作成されます。画像に個人情報などが含まれる可能性があるので、そのままSNSなどに公開しないでください。

### アンインストール

Windowsの **設定 → アプリ → インストールされているアプリ → OCR Auto Typer - Go Edition → アンインストール** から削除できます。

### ライセンス・利用上の注意

- 作者が独自に作成した本アプリは **[MIT License](LICENSE)** で配布しています。日本語参考訳は [LICENSE.ja.md](LICENSE.ja.md) をご覧ください。
- **MITライセンスはソースコードの公開を義務付けません。** 本リポジトリで配布するのはインストーラーのみです。
- 同梱する **Tesseract OCRにはApache License 2.0** が適用されます。依存DLL・学習データなどの第三者製コンポーネントには、それぞれ別のライセンス条件が適用される場合があります。**これらは本アプリのMITライセンスで再許諾されません。**
- インストーラーを公開・再配布する際は、実際に含まれる第三者コンポーネントの著作権表示、ライセンス全文、必要な通知文書を確認してください。
- 自動キー入力は**現在フォーカスされているウィンドウ**に送信されます。パスワード欄、チャット、業務アプリなどへの誤入力に注意してください。
- ソフトウェアは**無保証**で提供されます。第三者の利用条件を遵守してください。MITライセンスやREADMEの免責事項は、公式ゲームの使用禁止事項を解除するものではありません。

---

## English

### Overview

**OCR Auto Typer — Go Edition v1.0.2** is a Windows utility written in Go using native Windows APIs. It reads a selected, single line of Roman text using **Tesseract OCR** and sends simulated keystrokes to the currently focused application.

**Features:** mouse-driven screen region selection, OCR preview, start/stop controls, three speed presets (Stable / Fast / Ultra-fast), handling for `!`, `?` and trailing `i`, five-failure OCR stop, and a dedicated Go Edition icon.

### Requirements

- Windows 10 / 11, **64-bit**
- The Windows installer is designed to bundle the required Tesseract OCR components
- **No Python, Go SDK or .NET SDK is required** for end users
- Successful operation on every computer is not guaranteed

### Download and installation

1. Open the **Releases** page of this repository.
2. Under **v1.0.2 → Assets**, download `OCR-Auto-Typer-Go-Setup-1.0.2.exe`.
3. Verify the source of the downloaded file, then run the installer.
4. Follow the setup wizard and optionally create a desktop shortcut.
5. Open **OCR Auto Typer - Go Edition** from the Windows Start Menu.

> **Important:** **Code → Download ZIP** does not download the installer. Use **Releases → Assets**. Unsigned installers may trigger Windows SmartScreen warnings; do not run files from untrusted sources.

### How to use

1. Open a **local test page or application you have permission to automate** and display one line of Roman letters.
2. Press **F6** or use the region-select button, then drag to capture the entire line (including any trailing `i`).
3. Press **F7** to check OCR output if needed.
4. Click the intended input field/window and enable half-width Latin input.
5. Press **F8** to start and **F9** to stop.

| Key | Action |
| --- | --- |
| `F6` | Select an OCR region (Esc cancels selection) |
| `F7` | Preview recognized text and save a screenshot |
| `F8` | Start / resume typing |
| `F9` | Stop typing |
| `F10` | Cycle speed presets: Fast → Ultra-fast → Stable |
| `Ctrl + Shift + Q` | Exit the app |

### Changes in v1.0.2

- Slightly longer key-press duration for `i`, without slowing other characters
- Additional confirmation of words ending in `i`
- Retains the fix for Tesseract subprocess console windows from v1.0.1

### Troubleshooting

If OCR fails, select the entire line again with F6 and check the F7 preview. If typing is missing, focus the target field and enable Latin-character input. For a missed `i`, try Stable mode and leave extra space to the right of the selected text. The OCR selection overlay is primarily designed for the primary monitor. OCR normalization can confuse `l`, `1` and `i` in ordinary English words.

OCR preview images may be saved to `%LOCALAPPDATA%\OCR-Auto-Typer-Go\ocr_preview.png`. Do not publicly share screenshots containing sensitive data.

### Uninstall

Open **Windows Settings → Apps → Installed apps → OCR Auto Typer - Go Edition → Uninstall**.

### License and important notices

The original application is provided under the **[MIT License](LICENSE)**. A [Japanese reference translation](LICENSE.ja.md) is included. **The MIT License does not require the author to publish source code.** This repository distributes **only the compiled installer**, not the Go source files.

Bundled **Tesseract OCR is licensed under Apache License 2.0**. Additional native libraries and language data may carry different license requirements. They are **not relicensed under the MIT License**. Required third-party attributions, license texts and notices must be included in the distributed installer as applicable.

Automated keystrokes go to the currently focused window; do not type into sensitive fields accidentally. OCR and key injection are supplied **as is**, without any guarantee of accuracy or compatibility. Use only on authorized targets. Third-party service rules still apply; the MIT License does not grant permission to automate websites that forbid it.

**Official Sushi-Da / Neutral usage rules:** https://keyx0.net/about.html
