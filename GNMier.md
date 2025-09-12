# GNMiner(ルール抽出手法) と ItemSB(統計的に有意な相関ルール)

## GNMiner とは
**GNMiner (Genetic Network Miner)** は、遺伝的ネットワークプログラミング (GNP) を基盤とした進化的計算手法で、数値データを含むデータベースから **統計的に特徴的なルール** を効率的に発見するために開発されました【1】。

## 特徴
- **進化的探索**  
  GNP（Genetic Network Programming）の個体（ネットワーク構造）が世代を重ねる中で、  
  興味深いルールを逐次的に発見し、ルール集合を蓄積していく。  

- **ルール抽出の高速化**  
  Apriori や FP-growth のように「頻出アイテム集合」を事前に構築する必要がなく、  
  直接ルール（ALDR）を抽出できる。  

- **多様なルール表現**  
  - **1d-ALDR**: 連続変数1つの局所分布を表すルール  
  - **2d-ALDR**: 連続変数2つの同時分布を表すルール（本論文で提案）  

- **暗黙的メモリ機能**  
  GNPのノード遷移構造が探索の履歴を保持し、効率的に部分集合（属性組み合わせ）を探索可能。  

---

## ルール例

- **1d-ALDR**  
  ```math
  (A_1 = 1) ∧ (A_2 = 1) → (m_Y, s_Y)
もし属性 A1 と A2 が成り立つなら、Y の値は平均 m_Y、標準偏差 s_Y の分布を持つ。
- **2d-ALDR**
  ```math
(A_1 = 1) ∧ (A_2 = 1) → (m_X, s_X, m_Y, s_Y)
属性の組み合わせが、連続変数 X, Y の両方で狭い分布（標準偏差が小さい）をもつことを示す。

---

## ItemSB とは
**ItemSB (Itemsets with Statistically Distinctive Backgrounds)** は、**GNMinerが発見する統計的に有意な相関ルール**を指します【2】。  

従来の「頻出アイテム集合」では出現回数の多さに着目しますが、ItemSBでは **属性組み合わせが形成する小集団の統計的特徴**（平均・分散・相関など）に基づいてルールを発見します。

### 特徴
- **統計的背景をもつアイテム集合**  
  アイテム集合に対し、平均・分散・相関係数などの統計量を付与。  
- **欠損値を含むデータベースにも対応**  
  利用可能なインスタンスのみを計算に反映。  
- **コントラストItemSB**  
  2つのデータ群（例: Group AとGroup B）で統計的に異なる背景を持つアイテム集合も抽出可能。  

### ルール表現
`(A1 = 1) ∧ (A2 = 1) → (mX, sX, mY, sY, RXY)`
- mX, mY : 平均値  
- sX, sY : 標準偏差  
- RXY : 相関係数  

この表現により、単なる「共起」ではなく、**属性組み合わせが形成する小集団の統計的特徴**を理解できる。  

---

## 応用例
- 音楽データ＋地図データを用いた予測タスク:contentReference[oaicite:2]{index=2}  
- 医療データ（HCCデータセット）における生存/死亡と年齢の関係分析:contentReference[oaicite:3]{index=3}  
- 大規模データにおける相関発見と条件付きパターン抽出  

---

## 参考文献
- 【1】K. Shimada, T. Arahira, S. Matsuno, *Evolutionary Method for Two-dimensional Associative Local Distribution Rule Mining*, IEEE ICTAI 2021:contentReference[oaicite:4]{index=4}  
- 【2】K. Shimada, T. Arahira, S. Matsuno, *ItemSB: Itemsets with Statistically Distinctive Backgrounds Discovered by Evolutionary Method*, Int. J. Semantic Computing, 2022:contentReference[oaicite:5]{index=5}

