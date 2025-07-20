Estive pensando nessa ideia faz um tempo, comecei com "Hyper-grafos com Dependencias" mas logo reparei que havia relaçoes mais interessantes e mais generalizaveis implicação e implicação com negação, quis criar condiçoes mais interessantes que dependesse do caminho escolhido inventei a ideia de Ultra-Vertices (que é um conjunto de vertices), a ideia foi se expandindo e se tornou algo extremamente generalizavel.



# Ultragrafos com Relações

Um Ultragrafo com Relações é definido por $U = (V,H, E_V, R_V,M)$, onde:

$V$ é um conjunto finito de elementos chamados vértices (ou nós).

$H$ é um conjunto finito de conjunto disjuntos de vértices chamada de Ultra-vértices.

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

Suponha também que existam caminhos paralelos de um vértice inicial $s \in V$ para um vértice convergente $t \in V$ (fechamento de caminhos): um ramo passando por $v_i$ (permitindo $v_j$ e além), outro por $v_2 \in V$ (sem $v_i$, e portanto incapaz de ativar $v_j$ ou além devido à relação).

Os caminhos podem ser separados em com $v_i$ (válidos para além de $v_j$) e sem $v_i$ (limitados, não alcançando além de $v_j$).

Construa um ultragrafo $U' = (V', H', E_H', \emptyset, M')$ sem relações, onde:

- $V' = V \cup V_d$, com $V_d$ duplicata de vértices a partir do ponto de convergência $t$ e subgrafos além (incluindo duplicatas de $v_j^d$, $t^d$).

- $H' = \{ \{v\} \mid v \in V' \}$ (mantendo singletons para consistência com $U$).

- $E_H'$ inclui ultra-arestas (que são arestas simples, pois singletons):

     - Arestas originais de $E_H$ até a ramificação.
    - Para ramo com $v_i$: arestas para $v_j$, $t$, e subgrafo além.
    - Para ramo sem $v_i$ (via $v_2$): arestas para duplicatas $V_d$, mas com corte abrupto (sem arestas além do correspondente a $v_j^d$, representando proibição estrutural; hiper-arestas não necessárias, pois singletons, mas conexões pares preservadas via duplicatas).

- $M'(v) = M(v)$ para $v \in V$, $M'(v^d) = M(v)$ para $v^d \in V_d$.

#### Teorema: Existe tal ultragrafo $U'$ sem relações cujo conjunto de caminhos válidos $P_H$ e $P_V$ coincide com o de $U$ (modulo mapeamento de duplicatas para originais em caminhos válidos, preservando singletons).

## Esboço Prova:

A construção duplica o subgrafo pós-convergência para o ramo sem $v_i$, cortando continuidade além de $v_j^d$ via $E_H'$, simulando a dependência $\implies$ sem $R$.

 Caminhos em $U$ ativando $v_j$ ou além requerem $v_i$ pela relação em prefixos; em $U'$, ramos sem $v_i$ param abruptamente (sem ativação de subgrafos dependentes), enquanto com $v_i$ continuam. Valididade em $U'$ depende só de $E_H'$ e $M'$, replicando restrições.
 
 O mapeamento bijetivo colapsa duplicatas para originais em caminhos com $v_i$, preservando conjuntos. etc...etc.. etc... preciso formalizar.


 ---

 TODO: Eu ainda tenho que verificar se todas provas estão corretas e teoremas e defs.