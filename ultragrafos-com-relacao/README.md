Estive pensando nessa ideia faz um tempo, comecei com "Hyper-grafos com Dependencias" mas logo reparei que havia relaçoes mais interessantes e mais generalizaveis implicação e implicação com negação, quis criar condiçoes mais interessantes que dependesse do caminho escolhido inventei a ideia de Ultra-Vertices (que é um conjunto de vertices), a ideia foi se expandindo e se tornou algo extremamente generalizavel.



# Ultragrafos com Relações

Um Ultragrafo com Relações é definido por $U = (V,H, E_V, R_V,M)$, onde:

$V$ é um conjunto finito de elementos chamados vértices (ou nós).

$H$ é um conjunto finito de conjuntos que é uma partição das vértices chamada de Ultra-vértices.

$E_V$ é um conjunto de Ultra-arestas direcionadas, cada Ultra-aresta $e \in E$ é um par ordenado $e = (A_e, B_e)$, com $A_e, B_e \subseteq V$, $A_e \neq \emptyset$ e $B_e \neq \emptyset$.

Um Ultra-caminho $P_H$ de um Ultra-vértice $u$ para um Ultra-vértice $v$ em $U$ é uma sequência de Ultra-vértices $H$:

$$P_H = (w_0, w_1, \dots, w_k)$$

onde:

- $w_0 = u$ e $w_k = v$ (com $k \geq 1$) e $w_i \in H$

- $\forall i \in \{1, \dots, k\}, \exists e \in E_V$ tal que $e = (A_e, B_e) \wedge A_e \subseteq w_{i-1}  \wedge  B_e \subseteq w_i$

O conjunto de ultra-vértices no ultra-caminho $P_H$ é $UVert(P_H) = \{ w_0, w_1, \dots, w_k \}$.

Um Caminho $P_V$ induzido por $P_H$ é: 
$$P_V = (v_0, \dots, v_k)$$ 

- $v_i \in w_i$ para todo $i$
- $\forall i=1 \dots k: \exists (A_e, B_e) \in E_H$ tal que $v_{i-1} \in A_e \subseteq w_{i-1}$, $v_i \in B_e \subseteq w_i$.

O conjunto de vértices no caminho $P_V$ é $Vert(P_V) = \{ v_0, v_1, \dots, v_k \}$.

$R_V$ chamada de ultra-arestas de relação é um conjunto de ultra-arestas direcionadas, cada ultra-aresta de relação $d \in R_V$ é um tripo ordenado $d = (A_d, B_d, R_d)$, com $A_d, B_d \subseteq V$, $A_d \neq \emptyset$ e $B_d \neq \emptyset$ e $\mathbb{R} = \{\implies ,\not\!\!\!\implies\}$ e $R_V \in \mathbb{R}$.

$M: V \to \mathbb{N} \cup \{\infty\}$, onde $M(v)$ é o número máximo de visitas permitidas ao vértice $v$ em um caminho.

Um ultra-caminho $P_H = (w_0, \dots, w_k)$ é válido em Ultragrafo com Relações se, além de satisfazer as condições de ultra-arestas em $E_H$, todos os seus prefixos consecutivos $P_H' = (w_0, \dots, w_j)$ (para cada $1 \leq j \leq k$) satisfazem, definindo $P_H'' = (w_0, \dots, w_{j-1})$ se $j \geq 2$ (e $P_H''$ vazio se $j = 1$, com $\bigcup_{w \in UVert(P_H'')} w = \emptyset$):

- $\forall (A_d, B_d, \implies) \in R: (B_d \cap \bigcup_{w \in UVert(P_H')} w \neq \emptyset) \to (A_d \cap \bigcup_{w \in UVert(P_H')} w \neq \emptyset)$, e se $(B_d \cap \bigcup_{w \in UVert(P_H')} w \neq \emptyset) \wedge (B_d \cap \bigcup_{w \in UVert(P_H'')} w = \emptyset)$, então $(A_d \cap \bigcup_{w \in UVert(P_H'')} w \neq \emptyset)$.

- $\forall (A_d, B_d, \not\implies) \in R: (A_d \cap \bigcup_{w \in UVert(P_H')} w \neq \emptyset) \to (B_d \cap \bigcup_{w \in UVert(P_H')} w = \emptyset)$.

- $\forall v \in V: |\{ w \in UVert(P_H') \mid v \in w \}| \leq M(v)$.

Um caminho $P_V = (v_0, \dots, v_k)$ é válido se todos os seus prefixos consecutivos $P_V' = (v_0, \dots, v_j)$ (para cada $1 \leq j \leq k$) satisfazem, definindo $P_V'' = (v_0, \dots, v_{j-1})$ se $j \geq 2$ (e $P_V''$ vazio se $j = 1$, com $\{v_i \mid i \in \emptyset \} = \emptyset$):

- $\forall (A_d, B_d, \implies) \in R: (B_d \cap \{v_0, \dots, v_j\} \neq \emptyset) \to (A_d \cap \{v_0, \dots, v_j\} \neq \emptyset)$, e se $(B_d \cap \{v_0, \dots, v_j\} \neq \emptyset) \wedge (B_d \cap \{v_0, \dots, v_{j-1}\} = \emptyset)$, então $(A_d \cap \{v_0, \dots, v_{j-1}\} \neq \emptyset)$.

- $\forall (A_d, B_d, \not\implies) \in R: (A_d \cap \{v_0, \dots, v_j\} \neq \emptyset) \to (B_d \cap \{v_0, \dots, v_j\} = \emptyset)$.

- $\forall v \in V: |\{ i \mid 0 \leq i \leq j, v_i = v \}| \leq M(v)$.

## Teorema 1.0 (Contradição por Implicação Ciclica)

Seja $S_R = \bigcup_{(A_d, B_d, \implies) \in R} \{ A_d, B_d \}$.

Seja $G_{+} = (S_R, E_R)$ o grafo dirigido com $E_R = \{ (A_d, B_d) \mid (A_d, B_d, \implies) \in R \}$.

Se $G_{+}$ contém um ciclo dirigido, então não existe $P_H$ válido nem $P_V$ válido em $U$ que comece de um ultra-vértice $u$ ou vértice $v_0$ tal que os vértices ativados no início não pertençam aos conjuntos do ciclo (i.e., $u \cap \left( \bigcup_{S_i \in C} S_i \right) = \emptyset$ para $P_H$, ou $v_0 \notin \bigcup_{S_i \in C} S_i$ para $P_V$, onde $C$ é o ciclo).

### Prova 1

Por absurdo. Foco em $P_H$ (análoga para $P_V$).

Suponha $P_H = (w_0, \dots, w_k)$ válido com $w_0 \cap \left( \bigcup_{S_i \in C} S_i \right) = \emptyset$, e suponha que o caminho ativa algum $S_l \in C$ em algum $t_{S_l} > 0$.

Como o caminho entra no ciclo de fora, seja $S_l$ o primeiro conjunto do ciclo ativado, com $t_{S_l} = \min \{ t_S \mid S \in C \}$.

Pela estrutura do ciclo, existe $S_m \to S_l$ (pois todo vértice em ciclo tem dependencia), então pela condição estrita para $(S_m, S_l, \implies)$, em $j = t_{S_l}$, $S_m \cap \bigcup_{l=0}^{j-1} w_l \neq \emptyset$.

Mas $t_{S_m} < t_{S_l}$, contradizendo a minimalidade de $t_{S_l}$ (pois $S_m \in C$).
Propagando para trás no ciclo, a entrada de fora requer uma ativação prévia dentro do ciclo, impossível sem violar a minimalidade ou a estrita precedência.

Assim, nenhum caminho de fora pode entrar no ciclo sem contradição, implicando ausência de tais $P_H$ válidos.

### Q.E.D.

## Teorema 2.0 (Troca de Relaçoes Inversas caminhos paralelos)

Seja $U = (V, H, E_H, R, M)$ um ultragrafo com relações, onde:

- Existem vértices iniciais $i \in V$, finais $f \in V$, e $v_r \in V$ tal que caminhos de $i$ para $v_r$ passam obrigatoriamente por $f$.

- Existem dois caminhos paralelos de $i$ para $f$: um via $v_1 \in V$ (i.e., arestas conectando $i \to v_1 \to f$), outro via $v_2 \in V$ (i.e., $i \to v_2 \to f$), sem arestas cruzadas ou alternativas.

- $R = \{ (A_1, A_r, \implies) \}$, onde $A_1 \subseteq V$ contém $v_1$ mas não $v_2$, e $A_r \subseteq V$ contém $v_r$.

- $M(v) = 1$ para todo $v \in V$ (proibindo repetições).
Arestas adicionais $f \to v_r$.

Seja $U' = (V, H, E_H, R', M)$, com $R' = \{ (A_2, A_r, \not\implies) \}$, onde $A_2 \subseteq V$ contém $v_2$ mas não $v_1$.


#### Teorema: Os conjuntos de ultra-caminhos válidos $P_H$ e caminhos válidos $P_V$ de ultra-vértices contendo $i$ para ultra-vértices contendo $v_r$ em $U$ coincidem com os de $U'$.

### Prova

Os possíveis ultra-caminhos candidatos de $\{i\}$ para $\{v_r\}$ são sequências passando por $\{v_1\}$ ou $\{v_2\}$, depois $\{f\}$, e $\{v_r\}$ (outros violam $E_H$ ou $M$).

Em $U$: Para caminhos via $v_1$, prefixos ativando $A_r$ (i.e., $v_r$) já ativam $A_1$ (via $v_1$), satisfazendo $\implies$. Para via $v_2$, ativa $A_r$ sem $A_1$, violando $\implies$.

Em $U'$: Para via $v_1$, $A_2$ não ativado, satisfazendo $\not\!\!\!\implies$ (premissa falsa). Para via $v_2$, ativa $A_2$ e $A_r$, violando $\not\!\!\!\implies$.

Logo, apenas caminhos via $v_1$ são válidos em ambos. Análogo para $P_V$.

### Q.E.D.

## Teorema 3.0 (Ultra-Grafos com Relaçoes Isomorficos a Ultragrafos sem Relaçoes)

Um ultragrafo com relações $U = (V, H, E_H, R, M)$ é tal que cada ultra-vértice em $H$ contém apenas um elemento (singleton), correspondente ao seu vértice respectivo em $V$ (i.e., $H = \{ \{v\} \mid v \in V \}$), simulando um grafo direcionado padrão com relações lógicas sobre ativações de vértices.

Suponha que exista uma relação $(A_i, A_j, \implies) \in R$, com $A_i = \{v_i\}$, $A_j = \{v_j\}$, tal que $v_i$ é necessária para qualquer caminho válido que contenha $v_j$ ou ative vértices além de $v_j$ em subgrafos dependentes.

Suponha também que existam caminhos paralelos de um vértice inicial $s \in V$ para um vértice convergente $t \in V$ (fechamento de caminhos): um ramo passando por $v_i$ (permitindo $v_j$ e além), outro por $v_x \in V$ (sem $v_i$, e portanto incapaz de ativar $v_j$ ou além devido à relação).

Os caminhos podem ser separados em com $v_i$ (válidos para além de $v_j$) e sem $v_i$ (limitados, não alcançando além de $v_j$).

Construa um ultragrafo $U' = (V', H', E_H', \emptyset, M')$ sem relações, onde:

- $V' = V \cup V_d$, com $V_d$ é inserido duplicata de vértices a partir do ponto de ramificação $s$ e subgrafos além (incluindo duplicatas de $v_j^d$, $t^d$) até chegar no vertice convergente $t$.

- defina uma função $\delta$ aonde $\delta(v)=\{v,v^d\}$ a partir do vertice de ramificação até vertice convergente e $\delta(v)=\{v\}$ para as demais areas do grafo, e assim e definimos  $H' = \{ \delta(v) \mid v \in V \}$ 

- $E_H'$ inclui ultra-arestas:

    - Ultra-arestas originais de $E_H$ até a ramificação.
    - Para ramo com $v_i$: ultra-arestas para $v_j$, $t$, e subgrafo além.
    - Para ramo sem $v_i$ (via $v_x$): ultra-arestas para duplicatas $V_d$ de forma similar sua vertices originatarias conectada com outras $v^d$ e $v_x$, mas com corte abrupto (sem ultra-arestas além do correspondente a $v_j^d$, representando proibição estrutural).

- $M'(v) = M(v)$ para $v \in V$, $M'(v^d) = M(v)$ para $v^d \in V_d$.

#### Teorema: Existe tal ultragrafo $U'$ sem relações cujo conjunto de ultra-caminhos válidos $P'_H$ coincide com o $P_V$ e $P_H$ de $U$ via mapeamente bijetivo. 
Exemplo.: $P'_H = \delta(P_v)$ e $P'_H = \delta(\pi(P_H))$ dado $\pi$ uma função que seleciona elemento em $V$ dentro de $w$.

## Esboço Prova:

A construção de $U'$ utiliza duplicatas nos ultra-vértices via $\delta$ para codificar "modos" de ativação: o modo original ($v$) para caminhos que satisfazem a relação $\implies$ (i.e., passando por $v_i$), e o modo duplicado ($v^d$) para caminhos que tentam violar a relação (sem $v_i$). 

Os ultra-vértices compostos $\delta(v) = \{v, v^d\}$ permitem escolha implícita no caminho induzido $P_V'$, mas as ultra-arestas $E_H'$ são definidas de forma a cortar progressão no modo duplicado após $v_j^d$, replicando a restrição lógica sem $R$.

Defina o mapeamento bijetivo $\phi: P_V(U) \to P_H'(U')$ (e similarmente para $P_H(U)$, pois $H$ são singletons, $P_H(U) \equiv P_V(U)$ via $\pi(w) = v \in w$) como $\phi(P_V) = (\delta(v_0), \delta(v_1), \dots, \delta(v_k))$, onde para caminhos válidos em $U$ (que passam por $v_i$ para ativar $v_j$ e além), a escolha no caminho induzido em $U'$ usa o modo original $v$; para tentativas inválidas, o modo $v^d$ é forçado pelo ramo via $v_x$, mas cortado.

#### Passo 1: Todo $P_V$ válido em $U$ mapeia para $P_H'$ válido em $U'$.

Seja $P_V = (v_0 = s, \dots, v_k)$ válido em $U$. 

Como válido, se ativa $v_j$ ou além, deve ter passado por $v_i$, satisfazendo $\implies$ em prefixos. 

O ramo é via $v_i$, então em $U'$, as ultra-arestas preservam conexões originais: $E_H'$ inclui arestas de $E_H$ para o modo original. Assim, $P_H' = \phi(P_V) = (\delta(v_0), \dots, \delta(v_k))$ satisfaz as condições de ultra-caminho em $E_H'$ (arestas originais conectam subconjuntos nos modos $v$), e as visitas respeitam $M'$ (idêntico a $M$). Como não usa modos $v^d$ (forçados apenas no ramo sem $v_i$), não há corte, e $P_H'$ é válido.

#### Passo 2: Todo $P_H'$ válido em $U'$ mapeia para $P_V$ válido em $U$.

Seja $P_H' = (w_0, \dots, w_k)$ válido em $U'$. 

Como $R = \emptyset$, validade depende só de $E_H'$ e $M'$. 

Defina o inverso $\phi^{-1}(P_H') = (\pi'(w_0), \dots, \pi'(w_k))$, onde $\pi'(w) = v$ se $w = {v}$ ou o componente original $v \in w = {v, v^d}$ (colapsando duplicatas para originais apenas se o caminho induzido usa modo válido). 

Para $P_H'$ válido que alcança além de $v_j$ (e.g., subgrafos dependentes), deve usar o modo original nos ultra-vértices $\delta(v)$, pois o modo $v^d$ é cortado em $E_H'$ após $v_j^d$ (sem arestas além). 

Caminhos que tentam modo $v^d$ (via ramo $v_x$) param em $v_j^d$, não alcançando o final. Assim, $P_H'$ válidos completos correspondem a caminhos usando modo $v$, que mapeiam para $P_V$ em $U$ via colapso, e como usam ramo $v_i$, satisfazem $\implies$ e outras condições (edges e $M$ preservados).

#### Passo 3: O mapeamento é bijetivo.

$\phi$ é injetivo: caminhos distintos em $U$ levantam para ultra-caminhos distintos em $U'$ (modos originais preservam estrutura). Surjetivo sobre válidos: todo $P_H'$ válido em $U'$ usa modo original (como duplicados cortam), colapsando bijetivamente para $P_V$ válido em $U$. Exemplo: $P'_H = \delta(P_V)$ preserva validade, e $\phi^{-1} = \pi \circ \delta^{-1}$ (selecionando original).

Portanto, os conjuntos coincidem via o mapeamento. 

etc...etc.. etc... preciso formalizar melhor e verificar todos os passos.


 ---

 TODO: Eu ainda tenho que verificar se todas provas estão corretas e teoremas e defs.