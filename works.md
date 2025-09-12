# 成果物

## GNMierによるルール抽出と最適化

### 概要
- **目的**: GNMier を用いて発見したルール集合を組み合わせ、  
  さらにルール間の論理的つながりを最適化するアルゴリズムを実装。  
- **特徴**:
  - サポート・スコアに基づくルール評価
  - GNP（Genetic Network Programming）の進化的操作を利用
  - ルール間の接続構造を探索し、最適なネットワークを構築

### 主なコード
- `gnmier_rule_optimize.py`  
  - GNMier で抽出されたルール群を入力  
  - ルール間の論理的つながりを探索・最適化  
  - ネットワーク構造として出力（可視化にも対応予定）

### 実行例
```bash
python gnmier_rule_optimize.py rules_input.txt optimized_rules.json
