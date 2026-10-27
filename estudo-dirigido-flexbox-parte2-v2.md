# Estudo Dirigido – CSS: Flexbox (parte 2)

Davi Gehart Vicente – 1F
Técnico Integrado em Informática para Internet
Prof. Hewerton Enes de Oliveira – 2026

---

## 1. Revisão da parte 1

1. O contêiner é o pai, que organiza o que tem dentro. Os itens são os filhos diretos dele. O `display: flex` vai no contêiner.

2. O eixo principal é o horizontal, indo da esquerda pra direita, porque o padrão do `flex-direction` é `row`.

---

## 2. Crescer: flex-grow

3. A sobra é o espaço que fica vazio na faixa depois de somar o tamanho dos itens. Se todos têm `flex-grow: 0`, ninguém ocupa essa sobra, então quem posiciona ela é o `justify-content`.

4. O valor padrão é **0**, o que significa que o item **não cresce**, fica só do tamanho que já tem.

5. A mesa é a faixa (o contêiner). O prato de cada pessoa é o tamanho de cada item. A sobra é a pizza, o que sobrou pra repartir. O peso do flex-grow é quantas fatias cada um leva.

6. Vai no elemento da marca:

```css
.marca { flex-grow: 1; }
```

Assim a marca pega toda a sobra e os links ficam do tamanho do texto.

7. Soma dos pesos: 2 + 3 + 1 = 6
Uma parte: 600 ÷ 6 = 100px
Larguras: 2 × 100 = 200px, 3 × 100 = 300px e 1 × 100 = 100px.

8. Sobra: 600 − (3 × 100) = 300px
Soma dos pesos: 0 + 1 + 2 = 3
Uma parte: 300 ÷ 3 = 100px
Larguras: 100 + 0 = 100px, 100 + 100 = 200px e 100 + 200 = 300px.

---

## 3. Encolher: flex-shrink

9. Quando falta espaço. O padrão é 1.

10. Os dois juntos dão 800px e a faixa tem 600px, então faltam 200px. Como são iguais, cada um perde 100px. Cada um fica com 300px.

11. O primeiro não encolhe, fica com 400px. O segundo perde os 200px todos: 400 − 200 = 200px. Os dois somam 600px, então cabe na faixa.

12. O logo de uma barra de navegação. Se ele encolhesse junto com o resto, a imagem ia ficar espremida. Com `flex-shrink: 0` ele mantém o tamanho.

---

## 4. Tamanho de partida e atalho flex

13. O `flex-basis` é o tamanho de partida do item, antes de repartir a sobra ou cortar o que falta. O `flex-basis` ganha do `width`, então vale o 10rem (160px).

14. Porque com base 0 todos os itens começam com tamanho zero, aí a sobra é a faixa inteira, e o `flex-grow` reparte tudo.

15.

| Atalho | grow | shrink | basis |
| --- | --- | --- | --- |
| flex: initial | 0 | 1 | auto |
| flex: 1 | 1 | 1 | 0 |
| flex: auto | 1 | 1 | auto |
| flex: none | 0 | 0 | auto |

16. Com `flex: 1`: a base é 0 pros dois, então a sobra é 600px. Cada um leva metade, 300px e 300px.

Com `flex: auto`: as bases são 100 e 300, somando 400. Sobra 600 − 400 = 200px, metade pra cada (100px). Fica 100 + 100 = 200px e 300 + 100 = 400px.

Dá diferente porque o `flex: 1` começa do zero e ignora o conteúdo, e o `flex: auto` começa do tamanho do conteúdo e só reparte a sobra.

17. Verdadeiro. Se o conteúdo é igual, a base do `auto` é igual pros dois e a sobra é dividida igualmente, então todos ficam do mesmo tamanho, igual ao `flex: 1`. A diferença só aparece quando o conteúdo é diferente, como na 16.

---

## 5. O mínimo que trava o encolhimento

18. Quem segura é o `min-width: auto`, que é o padrão dos itens flex e não deixa o item ficar menor que o conteúdo. Pra soltar, coloca `min-width: 0` no item.

19. No `main` com o texto, do lado do `aside` com o menu, quando tem uma palavra, link, tabela ou código muito grande. Sem o `min-width: 0` o texto não encolhe e empurra a página pra fora.

---

## 6. order e align-self

20.
(a) Na tela fica C, A, B, porque o `order: -1` joga o C pro começo.
(b) Com Tab o foco segue a ordem do HTML, então é A, B, C.
(c) O leitor de tela também lê na ordem do HTML. Aí a pessoa ouve numa ordem e a tela mostra outra, e isso confunde.

21. O padrão é 0. Aparece primeiro o `order: -1`, porque vai do menor pro maior.

22. Com `align-self: flex-end` o filho ignora o stretch do pai, não estica e vai pro final do eixo transversal. Com `align-self: auto` ele segue o pai e continua esticado.

23. O `align-items` quando quero o mesmo alinhamento pra todos os itens. O `align-self` quando só um item precisa ser diferente.

---

## 7. A página com miolo

24. Itens de `.pagina`: o `header`, o `.miolo` e o `footer`.
Itens de `.miolo`: o `aside` e o `main`.

25. Porque o flex só vale pros filhos diretos. O `.miolo` ser item da `.pagina` não faz o `aside` e o `main` virarem itens. Pra isso ele mesmo precisa ter `display: flex`.

26.
- `.pagina`: `display: flex` faz ela ser um contêiner, `flex-direction: column` empilha topo, miolo e rodapé, e `min-height: 100vh` faz ela ter pelo menos a altura da tela.
- `.miolo`: `display: flex` deixa menu e texto lado a lado, e `flex: 1` faz ele ocupar a sobra de altura, empurrando o rodapé pra baixo.
- `aside { flex: 0 0 10rem }`: o menu não cresce, não encolhe e tem largura fixa de 10rem.
- `main { flex: 1; min-width: 0 }`: o texto ocupa o resto da largura, e o `min-width: 0` deixa ele encolher sem estourar.

---

## 8. Erros comuns e síntese

27. O erro é que o `flex-grow` é propriedade de item, não de contêiner. O certo é deixar `display: flex` no pai e colocar o `flex-grow: 1` no filho que tem que crescer.

28. Primeiro, o `min-width: 0` no item. Serve quando o item tem que continuar na mesma linha e só precisa poder encolher, como um texto grande do lado de um menu. Segundo, o `flex-wrap: wrap` no contêiner. Serve quando os itens podem ir pra linha de baixo, como cartões ou botões.

29.
- `flex-basis`: o tamanho de partida do item.
- `flex-grow`: quanto da sobra o item ganha.
- `flex-shrink`: quanto o item cede quando falta espaço.
- `order`: muda a ordem visual dos itens sem mexer no HTML.
- `align-self`: muda o alinhamento de um item só, ignorando o `align-items` do pai.
