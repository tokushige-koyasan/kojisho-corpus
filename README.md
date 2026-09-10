# kojisho-corpus

平安時代漢字字書総合データベース（HDIC: Integrated Database of Hanzi Dictionaries in Early Japan、池田証壽代表）が CC BY-SA 4.0 で公開している日本古辞書・中国字書のテキストデータを、原ファイル無加工のまま一括収録し、catalog.csv を付した再配布コーパスである。

収録辞書（6種、TSV/TXT 19ファイル）

| 略号 | 書名 | 撰者・成立 | 底本 | 収録ファイル |
|---|---|---|---|---|
| KTB | 篆隷万象名義 | 空海、c. 827–835 | 高山寺本 | KTB.tsv（全文）、KTB_entries.txt（見出し一覧）、KTB_ndl.txt（NDL画像対応）、KTB_ndl_Seal.tsv（篆書字IIIF座標） |
| TSJ | 新撰字鏡 | 昌住、c. 898–901 | 天治本（1124写、宮内庁書陵部蔵） | TSJ_entries.tsv（見出し全一覧）、TSJ_definitions.tsv（見出し＋注文）、TSJ_wakun.tsv（和訓）、TSJ_ndl.tsv（画像対応） |
| SYP | 宋本玉篇（大広益会玉篇） | 陳彭年ほか、1013 | 澤存堂本（書陵部蔵南宋版との差異を併記） | SYP.tsv（全文）、SYP_keio.tsv（書陵部本IIIF対応） |
| YYP | 原本玉篇残巻 | 顧野王、543（唐写本残巻） | 日本伝存残巻（巻8・9・18・19・22・24・27） | YYP.tsv（全文、暫定）、YQF.tsv（逸文、上流で準備中・データ行なし） |
| GLS | 龍龕手鏡 | 行均、997 | 高麗本 | GLS_ndl.txt（部首→NDL画像対応のみ。本文は上流で準備中） |
| KRM | 観智院本類聚名義抄 | 撰者未詳（真言宗僧）、12世紀後半 | 観智院本（天理図書館蔵） | krm_main.tsv（基本データ）、krm_notes.tsv（注文分解）、krm_headword_chars.tsv（掲出字構成文字）、krm_wakun.tsv（和訓）、krm_pronunciations.tsv（音注）、krm_ndl.tsv（画像対応） |

各ファイルの版番号・公開日・最終更新日・行数・SHA-256 は catalog.csv を参照。KRM のカラム仕様は dicts/KRM/docs/data_specification_jp.md（英語版 data_specification.md）に上流の仕様書を同梱した。

## 構成

```
kojisho-corpus/
├── README.md
├── LICENSE                 CC BY-SA 4.0（上流の LICENSE をそのまま継承）
├── NOTICE_HDIC.md          上流 HDIC project および各データ担当者の帰属表示
├── catalog.csv             ファイル単位の目録（19行、UTF-8・LF）
├── dicts/
│   ├── KTB/  TSJ/  SYP/  YYP/  GLS/    shikeda/HDIC 由来
│   └── KRM/  (+ docs/)                 shikeda/krm 由来
└── verification/
    ├── SHA256SUMS.txt      収録全ファイルの SHA-256
    └── upstream_snapshot.txt  上流コミットSHA・不採用ファイルの記録
```

## 上流と収録の方針

- 上流：https://github.com/shikeda/HDIC （master）および https://github.com/shikeda/krm （main）。取得時のコミットSHAは catalog.csv の upstream_commit 列と verification/upstream_snapshot.txt に記録した。
- 原ファイルは無加工で収録する（改行コードは LF に正規化する方針だが、上流に CR/CRLF は存在せず、収録ファイルはすべて上流とバイト同一である）。各ファイル冒頭の `#` コメントヘッダー（版番号・日付・著作権表示・連絡先・カラム凡例）もそのまま保持している。
- 観智院本類聚名義抄は、HDIC リポジトリに同梱されている旧版（KRM.tsv v1.1.347・KRM_definitions.tsv・KRM_wakun.tsv・KRM_ndl.txt、2025年3月で更新終了）ではなく、仕様変更後の改訂版を公開している shikeda/krm の TSV を採用した。krm の JSON はTSVからの派生物、scripts/・webapp/ はMITライセンスのツールであるため収録しない。
- 上流 HDIC の images/・samples/・v1.2/（krm への移転案内のみ）は対象外とした。
- ヘッダー記載の連絡先は上流のとおり。データ内容への照会は HDIC project（上流リポジトリ）へ。本リポジトリは再配布のみを行い、データの修正・校正は行っていない。

## 更新

上流の更新（KTB.tsv 等の Version 行、krm の最終更新日）を定期的に確認し、差分があれば版を上げて再収録する。上流の改訂履歴は各ファイルのヘッダーおよび上流リポジトリのコミット履歴を参照。

## ライセンスと帰属表示

本リポジトリの dicts/ 以下のデータは、上流の Creative Commons Attribution-ShareAlike 4.0 International（CC BY-SA 4.0）を継承する。利用にあたっては NOTICE_HDIC.md の帰属表示を保持すること。catalog.csv・README・verification/ も同ライセンスとする。

データを研究に用いる場合は、本リポジトリではなく上流の HDIC project を典拠として引用すること。引用例：

- HDIC project（池田証壽代表）「平安時代漢字字書総合データベース」https://github.com/shikeda/HDIC （各ファイルの版番号・日付はヘッダー参照）
- Ikeda, Shōju. (2026). *KRM: Database of the Kanchi-in Manuscript of the Ruiju Myōgishō*. Version v1.2.7. Zenodo. https://doi.org/10.5281/zenodo.22164768 （本リポジトリ収録の krm TSV は v1.2.7 以後の GitHub 現行版であり、Zenodo 版とは細部が異なる。学術引用は上流の指示に従い Zenodo 版を用いること）
