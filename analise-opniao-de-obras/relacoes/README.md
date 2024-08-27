# Relações

# Betwenness (Definição de Peter Gärdenfors, 2000)

Uma das forma de relação axiomatica simples do conceito de "entre dois objetos" é relação terciaria $ \mathcal{B}(A, B, C)$.

Esse conceito pode ser utilizado para generalizar a noção de betweenness em diferentes contextos matemáticos, como em geometria e teoria dos grafos.

Os axiomas (que eu mesmo nomei) que definem o relação de Betwenness são:

1. **Axioma da Distinção**
 $$\mathcal{B}(A, B, C) \implies A, B, C \text{ são objetos distintos}$$

2. **Axioma da Simetria**
$$\mathcal{B}(A, B, C) \implies \mathcal{B}(C, B, A)$$

3. **Axioma da Assimetria Interna**

$$\mathcal{B}(A, B, C) \implies \lnot \mathcal{B}(B, A, C)$$


4. **Axioma da Transitividade**

$$
\mathcal{B}(A, B, C) \land \mathcal{B}(B, C, D) \implies \mathcal{B}(A, B, D),
$$



