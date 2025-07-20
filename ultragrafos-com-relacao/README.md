Estive pensando nessa ideia faz um tempo, comecei com "Hyper-grafos com Dependencias" mas logo reparei que havia relaçoes mais interessantes e mais generalizaveis implicação e implicação com negação, quis criar condiçoes mais interessantes que dependesse do caminho escolhido inventei a ideia de Ultra-Vertices (que é um conjunto de vertices), a ideia foi se expandindo e se tornou algo extremamente generalizavel.




# Ultragrafos com Relações.

Um Ultragrafo com Relações é definido por $U = (V,H, E_V, R_V,M)$, onde:

$ V $ é um conjunto finito de elementos chamados vértices (ou nós).

$ H $ é um conjunto finito de conjunto disjuntos de vértices chamada de Ultra-vértices.

$ E_V $ é um conjunto de Ultra-arestas direcionadas, cada Ultra-aresta $ e \in E $ é um par ordenado $ e = (A_e, B_e) $, com $ A_e, B_e \subseteq V $, $ A_e \neq \emptyset $ e $ B_e \neq \emptyset $.

Um Ultra-caminho $P$ de um Ultra-vértice $ u $ para um Ultra-vértice $ v $ em $ U $ é uma sequência de Ultra-vértices $H$:

$$P = (w_0, w_1, \dots, w_k)$$

onde:

- $ w_0 = u $ e $ w_k = v $ (com $ k \geq 1 $) e $w_i \in H$

- $ \forall i \in \{1, \dots, k\}, \exists e \in E_V $ tal que $ e = (A_e, B_e) \wedge A_e \subseteq w_{i-1}  \wedge  B_e \subseteq w_i $

O conjunto de ultra-vértices no ultra-caminho $ P $ é $ UVert(P) = \{ w_0, w_1, \dots, w_k \} $.

$ R_V $ chamada de ultra-arestas de relação é um conjunto de ultra-arestas direcionadas, cada ultra-aresta de relação $ d \in R_V $ é um tripo ordenado $ d = (A_d, B_d, R_d) $, com $ A_d, B_d \subseteq V $, $ A_d \neq \emptyset $ e $ B_d \neq \emptyset $ e $ \mathbb{R} = \{\implies ,\not\!\!\!\implies\}$ e $R_V \in \mathbb{R}$.

$ M: V \to \mathbb{N} \cup \{\infty\} $, onde $ M(v) $ é o número máximo de visitas permitidas ao vértice $ v $ em um caminho.

Um ultra-caminho $ P $ válido em Ultra-grafo com Relações é somente se:

- $ \forall (A_d, B_d, \implies) \in R: (A_d \cap \bigcup_{w \in UVert(P)} w \neq \emptyset) \to (B_d \cap \bigcup_{w \in UVert(P)} w \neq \emptyset) $

- $ \forall (A_d, B_d, \not\!\!\!\implies) \in R: (A_d \cap \bigcup_{w \in UVert(P)} w \neq \emptyset) \to (B_d \cap \bigcup_{w \in UVert(P)} w = \emptyset) $

- $ \forall v \in V: |\{ w \in UVert(P) \mid v \in w \}| \leq M(v) $



