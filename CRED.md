# CRED: Continuous/discrete Rule Extractor via Decision Tree Induction

CRED は、ニューラルネットワークの学習済みモデルから **if-then 形式のルール** を抽出する手法です。  
従来手法と比べて、**連続値 (continuous)** と **離散値 (discrete)** の両方を扱える点が特徴です。  

---

## 背景

- ニューラルネットワークは高精度だが「ブラックボックス」で解釈が難しい  
- ルール抽出により、入力と出力の関係を **人間が理解できる形** で表現可能  
- CRED は決定木を用いた **分解型アプローチ (decompositional method)** に基づき、隠れ層の役割まで説明できる  

---

## アルゴリズムの流れ

CRED は以下の 5 ステップで構成されます：

1. **ターゲットクラス設定**  
   - 出力ユニットの活性値を離散化し、分類対象クラスを決定

2. **Hidden-Output Tree 構築**  
   - 隠れユニットの活性を特徴量とし、決定木を学習  
   - 中間ルール（intermediate rules）を抽出

3. **Input-Hidden Tree 構築**  
   - 入力層と隠れ層の対応関係を決定木で学習  
   - 入力ルールを抽出

4. **ルール統合**  
   - 中間ルールに入力ルールを代入し、入力→出力のルールを生成

5. **ルール簡約化 (Generalization)**  
   - J-measure に基づいて不要な条件を削除・連続区間を統合  
   - 例: `(Age:30..39) + (NumCars:2..3)` と `(Age:45..49) + (NumCars:2..3)` を  
     `(Age:30..49) + (NumCars:2..3)` にまとめる

---

## 特徴

- **ブラックボックスの解消**：ニューラルネットワークの予測根拠を人間可読なルールに変換  
- **連続値＋離散値対応**：実データに多い混合型の属性に適用可能  
- **隠れユニットの解釈**：各ユニットがどのような条件判別を担っているかを明示  
- **高い忠実度**：UCI データセットで高い分類精度を再現

---

## 実験結果（原著論文より）

- UCIリポジトリの複数データセットで検証  
- 例：**Credit Data**  
  - 抽出ルールで分類したサンプルの **99%** が NN の出力と一致  
  - 重要変数：`work-year`, `live-in-pr`, `sex`, `jobless`

---

## 参考文献

Makoto Sato, Hiroshi Tsukimoto,  
*Rule Extraction from Neural Networks via Decision Tree Induction*,  
**Proc. IEEE Int. Conf. Systems, Man, and Cybernetics**, pp. 1870–1875, 2001.  

---

