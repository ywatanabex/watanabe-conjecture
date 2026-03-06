# Watanabe予想（独立集合多項式とグラフ被覆）研究ノート：現時点の全まとめ（継続用）

> このファイルは、これまでの議論・証明・方針を **研究を継続できる形**で一箇所に集約したものです。  
> **重要**：本チャットの過程で「計算で確認した」と書いた内容の一部は、実際の実行ログがこの会話内に残っていないため、ここでは **(A) 厳密に証明済み** / **(B) 仕掛け（証明スケッチ）** / **(C) 計算で要検証** を明確に区別して記します。

---

## 0. 原典と参照

- 原典PDF：**“A conjecture on independent sets and graph covers” (Yusuke Watanabe)**  
  Conjecture 1 が主対象。M-cover を permutation voltage assignment で構成し、独立集合多項式の係数不等式を予想している。  
  （本チャットでは `Conjecture.pdf` として提供）  
- これまでの暫定メモ：`watanabe_summary_next_steps.md`（注意書き付き）

---

## 1. 定義とWatanabe予想（係数版）

### 1.1 M-cover（電圧割当による明示構成）

有限グラフ \(G=(V,E)\)。有向辺集合 \(\vec E\) を作り、電圧割当
\[
\alpha:\vec E\to S_M,\qquad \alpha(u\to v)=\alpha(v\to u)^{-1}
\]
を与える。被覆グラフ \(\tilde G=(\tilde V,\tilde E)\) は
\[
\tilde V=V\times [M],\quad (v,k)(u,\ell)\in\tilde E \iff uv\in E \ \&\ \ell=\alpha(v\to u)(k)
\]
で定義される。恒等置換を全辺に貼ったものが **trivial cover** \(G^{\oplus M}\)。  
（原典PDFの(1)(2)）

### 1.2 独立集合多項式（多変数）

\[
p(G)=\sum_{I:\text{independent}} \prod_{v\in I} x_v.
\]
（原典PDFの(3)）

### 1.3 射影 \(\pi\)

\(\pi:\tilde V\to V\) は層番号を忘れる写像。多項式では \(\pi(x_{(v,k)})=x_v\) で誘導。

### 1.4 Watanabe予想（Conjecture 1）

二部グラフ \(G\) と任意の M-cover \(\tilde G\) に対して
\[
\pi(p(\tilde G))\ \preceq\ p(G)^M
\]
（すべての単項式係数での不等式）。  
原典では等価な言い換えとして、任意の \(U\subseteq V\) について
\[
|I(\tilde G,\tilde U)| \le |I(G^{\oplus M},U)|
\]
を述べる（ただしこちらは「像が集合 \(U\)」に一致する独立集合を束ねた数え上げ）。  
（原典PDFの(4)(5)）

---

## 2. 係数の組合せ的読み替え（重要：係数版を扱う基本形）

指数ベクトル \(a=(a_v)_{v\in V}\)（各 \(0\le a_v\le M\)）を固定する。  
\([x^a]\pi(p(\tilde G))\) は次の数え上げに一致する：

- 各 \(v\in V\) に部分集合 \(S_v\subset [M]\) を割り当てて \(|S_v|=a_v\)
- 各辺 \(uv\in E\) に対し、独立性は
  \[
  S_v\ \cap\ \alpha(u\to v)(S_u)=\varnothing
  \tag{Edge-Disjoint}
  \]
  と同値（cover の隣接規則をそのまま集合版にしたもの）

よって
\[
[x^a]\pi(p(\tilde G))=
\#\{(S_v)_v:\ |S_v|=a_v,\ \text{(Edge-Disjoint)を満たす}\}.
\]
trivial cover では \(\alpha=\mathrm{id}\) なので制約は \(S_u\cap S_v=\varnothing\)。

> **観察（ゼロ判定）**：もしある辺 \(uv\) で \(a_u+a_v>M\) なら、trivial cover でも \(S_u\cap S_v=\varnothing\) は不可能なので右辺係数は0。cover側も同様に0（\(\alpha\) は全単射なので disjoint は同様に不可能）。  
> よってこの種のケースは両辺0で自明。

---

## 3. Gauge（共役）による正規化と holonomy

電圧割当 \(\alpha\) は頂点ごとの置換 \(g_v\in S_M\) による gauge 変換
\[
\alpha(u\to v)\mapsto g_v\,\alpha(u\to v)\,g_u^{-1}
\]
で同型な cover を与える（係数は不変）。

- スパニングツリー上の辺の電圧は gauge で全て恒等にできる。
- 残る独立パラメータは cycle rank \(|E|-|V|+1\) 本分の辺に集約できる。
- サイクル上の holonomy（辺置換の積）は gauge 不変量として現れる。

---

## 4. occupancy=1（平方自由係数）への縮約：対応彩色

### 4.1 occupancy=1 とは

平方自由単項式 \(x_U=\prod_{v\in U} x_v\) の係数。  
集合版では各 \(v\in U\) で \(|S_v|=1\)、\(v\notin U\) で \(|S_v|=0\)。

\(|S_v|=1\) のとき、選ばれた要素を \(\varphi(v)\in[M]\) と書くと、辺制約 (Edge-Disjoint) は
\[
\varphi(v)\neq \alpha(u\to v)(\varphi(u))
\tag{CSP}
\]
となる。これは **置換付き彩色（correspondence coloring）**。

- cover側：置換付き彩色数
- trivial側：通常の proper \(M\)-coloring 数

---

## 5. （A）厳密に証明済み：M=2 のとき Conjecture 1 は任意の二部グラフで成立

ここは本チャットで提示した重要定理。M=2 の特殊性 \(S_2\simeq\mathbb{Z}_2\) により線形化する。

### 5.1 主張

**定理（M=2 一般二部）**  
任意の二部グラフ \(G\) と任意の 2-cover \(\tilde G\) に対し
\[
\pi(p(\tilde G))\preceq p(G)^2
\]
が成り立つ（全係数）。

### 5.2 証明

係数 \([x^a]\) を固定。各 fiber は2点なので \(a_v\in\{0,1,2\}\)。

- \(a_v=0\)：何も選ばない  
- \(a_v=2\)：両層を選ぶ（自由度なし）  
- \(a_v=1\)：片方の層を選ぶ（自由度1ビット）

まず \(U_2=\{v:a_v=2\}\) があると、隣接頂点側では disjoint 制約で強い制限がかかるが、trivial cover でも同じ制限がかかるため、係数比較は「0=0」か「同じ形」に落ちる（厳密には、ある辺で \(a_u=2\) かつ \(a_v>0\) なら両辺係数0）。

従って本質は \(U_1=\{v:a_v=1\}\) の選択に集約される。  
\(v\in U_1\) について選ぶ層を \(\varphi(v)\in\{0,1\}\) とする。

2-cover の各有向辺には \(\alpha(e)\in S_2=\{\mathrm{id},\tau\}\)（swap）が付く。
独立性は各辺 \(uv\)（両端が \(U_1\) にいる場合）で
\[
\varphi(v)\neq \alpha(u\to v)(\varphi(u)).
\]
ここで \(\tau\) は \(\tau(x)=1-x\)。従ってこれは GF(2) で
\[
\varphi(u)+\varphi(v)=b_{uv}\pmod 2
\]
という一次方程式系になる（\(b_{uv}\in\{0,1\}\) は \(\alpha\) により決まる）。

連結成分ごとに一つ自由度があるか、サイクル矛盾で不可解（0個）かのどちらかで、
解数は
- 可解なら \(2^{c(H)}\)（\(H=G[U_1]\)、\(c(H)\)=連結成分数）
- 不可解なら 0

一方、trivial cover（\(\alpha=\mathrm{id}\)）側では二部グラフなので \(H\) は常に 2彩色可能、解数は常に \(2^{c(H)}\)。

よって係数ごとに cover側 \(\le\) trivial側、従って多項式係数不等式が成立。□

---

## 6. （A）厳密に証明済み：ladder（2×n はしご、開境界）で Conjecture 1（全係数）

ここは「この方針（DP＋単射）で」最も強い成果の一つ。

### 6.1 対象：open ladder \(L_n\)

頂点は上段 \(T_0,\dots,T_n\)、下段 \(B_0,\dots,B_n\)。  
辺：
- 上水平 \(T_iT_{i+1}\)
- 下水平 \(B_iB_{i+1}\)
- 縦 \(T_iB_i\)

### 6.2 gauge 正規形（ladder特有）

スパニングツリーとして「全縦辺＋全上水平辺」を取れば木になるので、gauge でそれらを恒等にできる。  
残るのは **下水平の n 本**だけで、そこに置換 \(\beta_i\in S_M\) が残る。

よって制約は列 \(i\) ごとに
- 縦：\(A_i\cap B_i=\varnothing\)
- 上：\(A_{i+1}\cap A_i=\varnothing\)
- 下：\(B_{i+1}\cap \beta_i(B_i)=\varnothing\)
（ここで \(A_i=S_{T_i}, B_i=S_{B_i}\)）

### 6.3 列DP（状態＝2集合）

係数ベクトル \(a\) を固定し、列 i のサイズは \(k_i=|A_i|, \ell_i=|B_i|\) で固定。

列遷移数（現在状態 \((A,B)\) から次状態 \((A',B')\) の作り方の個数）を数える。
現在状態 \((A,B)\) が与えられたとき、次列で必要なのは
\[
A'\cap A=\varnothing,\quad B'\cap \beta(B)=\varnothing,\quad A'\cap B'=\varnothing,
\]
かつ \(|A'|=k', |B'|=\ell'\)。

この数え上げは「禁止集合」 \(F_A=A,\ F_B=\beta(B)\) の **重なり**
\[
m:=|F_A\cap F_B|=|A\cap \beta(B)|
\]
だけに依存し、しかも \(m\) が大きいほど遷移数は減る（次節の補題）。

### 6.4 基本補題：2集合遷移数 \(d(m)\) の単調性（単射）

一般に、\(F_A,F_B\subset[M]\) を固定し、(i) \(A'\cap F_A=\varnothing\)、(ii) \(B'\cap F_B=\varnothing\)、(iii) \(A'\cap B'=\varnothing\)、(iv) サイズ固定 \(|A'|=k',|B'|=\ell'\) の解数を \(d(m)\) とする（\(m=|F_A\cap F_B|\)）。

領域分割：
- \(X=F_B\setminus F_A\)（A'専用）
- \(Y=F_A\setminus F_B\)（B'専用）
- \(Z=[M]\setminus(F_A\cup F_B)\)（共有：A'かB'かどちらか、両方は不可）

このとき生成関数で
\[
d(m)=[x^{k'}y^{\ell'}]\,(1+x)^{|X|}(1+y)^{|Y|}(1+x+y)^{|Z|}.
\]

**補題**：\(d(m)\) は \(m\) に関して非増加、特に \(d(m)\le d(0)\)。  
**証明**：\(m\to m-1\) で「共有領域Zから1要素を取り除き、A専用・B専用を各1増やす」操作を考える。共有要素 \(z_0\) が A' に入っていたらそれを専用要素 \(x_0\) に置換、B' に入っていたら \(y_0\) に置換、未使用ならそのまま、という写像を作ると単射になる。□

### 6.5 trivial cover が毎列で \(m=0\) を強制する

trivial cover では \(\beta=\mathrm{id}\)。縦制約で常に \(A\cap B=\varnothing\) なので
\[
m=|A\cap \beta(B)|=|A\cap B|=0
\]
が常に成立。従って各ステップで遷移数が最大（しかも一様）。

### 6.6 係数比較の結論

列DPで「部分割当総数」を \(N_i\) とすると
\[
N_{i+1}\le d_i(0)\,N_i,
\]
trivial では等号が成り立つため、終端で
\[
[x^a]\pi(p(\tilde L_n))\le [x^a]p(L_n)^M.
\]
係数 \(a\) 任意で成立するので Conjecture 1 が ladder で成立。□

---

## 7. （A）厳密に証明済み：ladder系の拡張（2-core が ladder／square-tree）

上の「2集合遷移＋単射」エンジンが効く範囲を最大化できる。

### 7.1 2-core が ladder のグラフ

ladderの各頂点に木（森林）を付け足しても、木部分はサイクルを持たないため gauge で電圧を消せる。さらに、係数抽出では根（接続点）での集合サイズが固定されるので、木部分の「完成数」は cover に依らない定数因子として分離できる。

結論：**2-core が ladder** なら Conjecture 1（全係数）が成立。

### 7.2 square-tree（四角形が木状に増殖するクラス）

4-cycle を「既存部分とちょうど1本の辺だけ共有して」木状に付け足していくクラスを \(\mathcal Q\) とする（ladder は特殊例）。

葉四角形（共有が1辺のみ）を一つ取り除くとき、共有2頂点の集合 \(S_u,S_v\) を固定した上で新2頂点 \(S_{u'},S_{v'}\) の数え上げが「2集合遷移問題」になり、trivial のとき重なりが最小（0）で最大化される、という同じ単射が局所的に働く。

帰納により：**square-tree の二部グラフは Conjecture 1（全係数）成立**。  
さらに木装飾も同様に吸収できるので、**2-core が square-tree** でも成立。

> ここまでが「この方針（単射で重なり単調）」で確実に押せる最大領域。

---

## 8. （A）厳密に証明済み：occupancy=1 でさらに広いクラス（cactus・θ など）

係数版全体ではなく occupancy=1 に限れば、別の行列トリック／固定点評価が効いてさらに広がる。

### 8.1 偶サイクルの公式（occupancy=1）

各辺 e の置換行列 \(P_e\)、全1行列 \(J\)、\(T_e=J-P_e\) とすると、サイクル上の置換付き彩色数は
\[
N=\mathrm{tr}\Bigl(\prod_{e\in C_{2k}} T_e\Bigr).
\]
rank-1 性質 \(J^2=MJ, JP=PJ=J\) を使うと積は
\[
\prod_e (J-P_e)=aJ + P(\beta)
\]
（偶長なので +）に潰れ、\(\beta\) は holonomy（辺置換の積）。固定点数 \(\mathrm{Fix}(\beta)\le M\) で trivial が最大と分かる。

### 8.2 cactus の貼り合わせ（occupancy=1）

サイクルが1頂点共有で木状に繋がる場合、共有頂点の色を固定して積に分解できる。各サイクルの寄与は
\[
L(c)=A+\mathbf{1}[c\in \mathrm{Fix}(\beta)]
\]
の2値構造（\(A\ge0\)）になり、展開係数が非負なので trivial が最大。

### 8.3 θ（2端点を複数パスで結ぶ）と “片側次数≤2” の一般化（occupancy=1）

- θでは各パスが端点色に対する核 \(K(i,j)=aJ\pm P(\beta)\) になり、並列合成は Hadamard 積。非負展開と固定点数の評価で trivial が最大。
- さらに「片側の次数 ≤2」の二部グラフでは、次数2側を消去すると制約が「等式（置換）付き」になり、Fortuin–Kasteleyn 型の正係数展開で trivial が最大になる。

> occupancy=1 は “色（1要素集合）”なので、固定点数・等式制約が扱いやすい。

---

## 9. 2×2格子（3×3頂点グリッド）について：本質的壁と最短戦略

ここが現在の最前線。2×2格子は 4つのC4が辺共有し、square-tree でも cactus でもない最小例。

### 9.1 gauge 正規形：自由度は4本置換に縮約

グリッドは \(|V|=9, |E|=12\) なので cycle rank は
\[
|E|-|V|+1=4.
\]
よって gauge によりスパニングツリー上の辺を恒等にし、残る **4本の辺**だけに置換を集約できる。

（例：縦辺＋上段横辺を木に入れ、残り4本を自由にする、など。）

### 9.2 ladder単射法が壊れる理由（構造）

ladder（幅2）では「列境界が2頂点」＝状態が2集合で済み、重なりパラメータが1個 \(m\) で閉じた。

2×2格子を列方向（3列）に切ると、中央列の境界が **3頂点**になり、状態は
\[
(A_{\text{top}},A_{\text{mid}},A_{\text{bot}})
\]
の3集合。次への遷移で衝突・禁止が多パラメータ化し、単一の重なり \(m\) では支配できない。

### 9.3 それでもこの方針で進める：境界DP＋Cauchy–Schwarz 還元（スケッチ）

3列グリッドを中央列で左右に分けると、係数カウントは中央境界状態 \(s\) 上で
\[
N(\text{cover})=\sum_s L(s)\,R(s)=\langle L,R\rangle
\]
と書ける。よって
\[
N^2 \le \langle L,L\rangle \,\langle R,R\rangle.
\]
この不等式は「一般 cover を左右対称 cover の幾何平均で上から押さえる」還元を与える：

- 左右で独立なねじれ（置換）があるとき、一般ケースは
  \[
  N(\sigma_0,\tau_0,\sigma_1,\tau_1)^2
  \le N(\sigma_0,\tau_0,\sigma_0,\tau_0)\cdot N(\sigma_1,\tau_1,\sigma_1,\tau_1)
  \]
  の形へ落とせる可能性がある（境界状態の内積構造から）。

残る核心は **左右対称 cover の最大化**：
\[
N(\sigma,\tau,\sigma,\tau)\ \le\ N(\mathrm{id},\mathrm{id},\mathrm{id},\mathrm{id})
\quad(\forall\sigma,\tau\in S_M).
\]
これが証明できれば、2×2格子の係数版 Conjecture 1 に到達する。

> ここは現在 (B) 証明スケッチ段階。完成には、境界状態空間の表現論（Terwilliger/partition algebra 的）か、多パラメータ単射（majorization）的補題が必要。

---

## 10. 計算検証について（C：要実行ログ）

本チャット中で「2×2格子の M=3 を全列挙で確認」等の発言が一部ありましたが、**この会話内に実行ログがなく、現時点では確定情報として扱えません**。

### 10.1 付属スクリプト

`grid2x2_M3_check.py`（このチャット環境に保存済み）を用意している。  
ただし、**このノートでは「そのスクリプトを実行し検証した」とは断定しない**。検証する場合は、以下の観点で再現性を確保すること：

- どの4辺を自由パラメータにした gauge 正規形か（スパニングツリーの明記）
- \(\pi(p(\tilde G))\) と \(p(G)^M\) の係数比較の実装が正しいか（独立集合カウントと射影の一致）
- 反例探索では、係数一点ではなく「全係数」の比較が必要（M=3 でも係数総数は \((M+1)^9\)）

---

## 11. 今後の最短ロードマップ（この方針を維持する）

### 11.1 2×2格子：まずやるべきこと（実験→補題抽出）

1. **M=2**：cycle rank 4なので2-lift（\(\mathbb{Z}_2^4\)）で正規形 16通りを全列挙し、係数版を完全比較。  
   → これが通れば「幅3でも少なくともM=2は真」を確定でき、一般 M の証明のヒントになる。
2. **M=3**：4辺自由なら \(6^4=1296\) cover を全走査可能。  
   ただし係数は \((4)^9\) と大きいので、実装最適化が要る（bitset など）。
3. 結果から「最悪 cover」や「差が出る係数パターン」を抽出し、証明の補題候補（どの重なり量が効くか）を立てる。

### 11.2 2×2格子：証明ターゲット（理論）

- Cauchy–Schwarz 還元を厳密に書く（境界状態空間の定義、左右分解の一意性）
- 対称 cover 最大化を、境界状態の軌道分解（\(S_M\) 作用の既約分解）で評価する  
  → 「置換行列の固有値は1の周りにある」では足りず、状態空間が \(k\)-subset を含むので Terwilliger 代数が出る。
- もし「単射法」が多パラメータで構築できるなら、それが最短（ただし難易度高）。

---

## 12. 付録：本ノートでの成果の分類（再掲）

### (A) 厳密に証明済み
- **M=2**：任意の二部グラフで Conjecture 1（全係数）
- **open ladder 2×n**：Conjecture 1（全係数）
- **2-core が ladder**：Conjecture 1（全係数）
- **square-tree（四角形が木状）**：Conjecture 1（全係数）
- **2-core が square-tree**：Conjecture 1（全係数）
- occupancy=1：
  - 偶サイクル：trivial 最大
  - cactus：貼り合わせで trivial 最大
  - θ／片側次数≤2：FK展開等で trivial 最大

### (B) 証明スケッチ／方針が具体的（未完成）
- 2×2格子：境界DP＋Cauchy–Schwarz 還元 → 対称 cover 最大化に帰着
- 境界状態空間の表現論（Terwilliger/partition algebra）を使う可能性

### (C) 計算で要検証（実行ログが必要）
- 2×2格子の M=3 全列挙確認など（スクリプトはあるが、実行確認は別途）

---

## 13. 参考：原典の含意（Bethe近似）

原典では Conjecture 1 が成り立つと、二値・ペアワイズ attractive model で
\[
Z \ge Z_B
\]
（真の分配関数が Bethe 近似以上）を導く（原典の Theorem 1）。  
この文脈では Conjecture 1 自体が中心。

---

## 14. 研究継続のための「次の具体作業リスト」

- [ ] 2×2格子（3×3頂点）で M=2 の全16 cover を列挙し、係数版 Conjecture 1 を全係数比較
- [ ] 2×2格子で M=3 の全1296 cover を列挙し、全係数比較（計算最適化）
- [ ] （通る場合）差が最大になる cover と係数を収集し、証明補題（単調性の多パラメータ版 or 表現論）候補を抽出
- [ ] Cauchy–Schwarz 還元の厳密化（境界状態の定義、左右分解の明確化）
- [ ] 対称 cover 最大化問題 \(N(\sigma,\tau,\sigma,\tau)\) の解析（小Mでパターン観察→一般化）

---

## 15. 付録：記号

- \(M\)：cover の層数
- \(\alpha:\vec E\to S_M\)：電圧割当
- \(S_v\subset[M]\)：頂点 \(v\) の fiber から選ぶ層集合
- \(\beta\)：サイクル holonomy（置換の積）
- \(\pi\)：層番号を忘れる射影
- \(\preceq\)：係数ごとの大小（dominance）

