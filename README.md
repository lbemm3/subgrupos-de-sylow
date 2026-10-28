[README_SYLOW.md](https://github.com/user-attachments/files/34102766/README_SYLOW.md)
# Verificador de Subgrupos de Sylow

Ferramenta interativa de **Álgebra Abstrata**, em um único arquivo HTML, que analisa a ordem |G| de um grupo finito e usa os **Teoremas de Sylow** (e alguns lemas auxiliares) para responder a perguntas como:

- Quais valores o número de p-subgrupos de Sylow nₚ pode assumir?
- Algum subgrupo de Sylow é **necessariamente normal** em qualquer grupo dessa ordem?
- Todo grupo dessa ordem **deixa de ser simples**? Por qual argumento?

Basta digitar a ordem do grupo. A página mostra a fatoração, os candidatos a nₚ, a justificativa teórica de cada conclusão e um resumo final. Tudo roda no navegador, sem instalação e sem internet.

🔗 **Acesse online:** <https://lbemm3.github.io/subgrupos-de-sylow/>

---

## Sumário

- [Funcionalidades](#funcionalidades)
- [Como usar](#como-usar)
- [O que a ferramenta mostra](#o-que-a-ferramenta-mostra)
- [Fundamentação matemática](#fundamentação-matemática)
- [Lógica de decisão](#lógica-de-decisão)
- [Exemplos](#exemplos)
- [Estrutura do código](#estrutura-do-código)
- [Limitações](#limitações)
- [Executando localmente](#executando-localmente)
- [Publicação via GitHub Pages](#publicação-via-github-pages)
- [Autoria e licença](#autoria-e-licença)

---

## Funcionalidades

- **Fatoração** da ordem |G| em primos, com exibição em notação de potências.
- **Candidatos a nₚ** para cada primo p que divide |G|, pelo 3º Teorema de Sylow (nₚ | b e nₚ ≡ 1 mod p, com |G| = pᵅ·b e p ∤ b).
- **Classificação de cada p-Sylow**: 🟢 *necessariamente normal* (nₚ = 1 é o único candidato) ou 🟡 *depende do grupo*.
- **Proposição do Índice**: para cada candidato nₚ > 1, verifica se |G| ∤ nₚ! e, quando isso vale para todos, conclui que G não é simples.
- **Argumento de contagem de elementos**, aplicado somente quando é matematicamente válido (veja [Limitações](#limitações)).
- **Casos especiais tratados diretamente**: ordem prima, p-grupos, ordens pq, pⁿq (com pⁿ < q) e pqr.
- **Conclusões estruturais**: quando todos os Sylows são normais, G é nilpotente e, se cada Sylow tem ordem p ou p², também abeliano.
- **Resumo final** com código de cores: verde, âmbar, azul ou cinza, conforme o resultado.
- **Painel de referência** recolhível com os teoremas e lemas usados.
- **Ordens notáveis** pré-carregadas: 12, 15, 28, 33, 56, 63, 72 e 20449.
- **Sem dependências**: HTML, CSS e JavaScript puro, que funciona offline e em celulares.

## Como usar

1. Abra a página (ou o `index.html` no navegador).
2. Digite a ordem do grupo no campo **Ordem do grupo |G|** (inteiro de 2 a 9.999.999), ou clique em uma das *ordens notáveis*.
3. Clique em **Analisar** (ou pressione **Enter**).
4. Leia as cartas por primo, as justificativas e o resumo.
5. Abra **📖 Referência** para consultar os enunciados dos teoremas e lemas.

A página abre com |G| = 72 já analisado.

## O que a ferramenta mostra

| Bloco | Conteúdo |
|---|---|
| **Fatoração** | |G| = p₁ᵅ¹ · p₂ᵅ² ⋯, e um aviso quando G é um p-grupo. |
| **Carta de cada p-Sylow** | Ordem pᵅ, decomposição |G| = pᵅ·b, restrições de nₚ, lista de candidatos (o valor 1 em destaque) e se o p-Sylow é necessariamente normal. |
| **Proposição do Índice** | Para cada nₚ > 1, a verificação |G| ∤ nₚ! (ou |G| | nₚ!) e se existe N ⊴ G não trivial. |
| **Aviso de contagem** | Quando α > 1, explica por que o argumento de contagem de elementos não se aplica. |
| **Caixas de argumento** | Lagrange, Lema 3.4, 3.5, 3.6, 3.7, contagem de elementos ou Proposição do Índice, conforme o caso. |
| **Conclusões sobre G** | Nilpotência e abelianidade, quando aplicáveis. |
| **Resumo** | 🟢 todos os Sylows normais · 🟠 G não é simples · 🔵 p-grupo · ⚪ nenhum Sylow necessariamente normal. |

## Fundamentação matemática

Seja G um grupo finito, p um primo que divide |G| e |G| = pᵅ · b com p ∤ b.

### Teoremas de Sylow

| | Enunciado |
|---|---|
| **1º (Existência)** | Se pᵐ divide |G|, então G tem subgrupo de ordem pᵐ. |
| **2º (Conjugação)** | Quaisquer dois p-Sylows de G são conjugados. |
| **3º (Contagem)** | O número nₚ de p-Sylows satisfaz nₚ | b e nₚ ≡ 1 (mod p). |
| **Cor. (Normalidade)** | Um p-Sylow é normal em G se e somente se nₚ = 1. |

### Proposição do Índice

Se H ≤ G tem índice [G : H] = n e |G| ∤ n!, então existe N ⊴ G com {1} ≠ N ⊆ H. Em particular, **G não é simples**.

A ferramenta aplica a proposição ao normalizador de um p-Sylow P, cujo índice é [G : N_G(P)] = nₚ. Se |G| ∤ nₚ! para todo candidato nₚ > 1, então, ou nₚ = 1 (Sylow normal), ou a proposição produz um normal não trivial. Nos dois casos, G não é simples. A divisibilidade |G| | k! é verificada por **valuações de Legendre**, sem calcular o fatorial.

### Lemas e teoremas auxiliares

| Referência | Enunciado |
|---|---|
| **Lagrange** | |G| primo ⟹ os únicos subgrupos são {1} e G; logo G é simples. |
| **Teorema 2.2** | Se G é p-grupo não trivial, então Z(G) ≠ {1}. |
| **Lema 1.9** | Todo grupo de ordem p² é abeliano. |
| **Lema 3.4** | |G| = pq, com p < q primos ⟹ n_q = 1 ⟹ G não é simples. |
| **Lema 3.5** | |G| = pqr, com p < q < r primos ⟹ algum Sylow é normal (por contagem de elementos). |
| **Lema 3.6** | |G| = pⁿq com pⁿ < q ⟹ n_q = 1 ⟹ o q-Sylow é normal. |
| **Lema 3.7** | G é p-grupo com |G| = pᵏ, k > 1 ⟹ G não é simples (subgrupo de ordem p, se abeliano; Z(G), se não abeliano). |

A numeração segue a referência embutida na própria ferramenta.

### Observação sobre contagem de elementos

Se o p-Sylow tem ordem prima (α = 1), dois p-Sylows distintos se intersectam apenas na identidade, e há exatamente nₚ·(p − 1) elementos de ordem p. Se α > 1, p-Sylows distintos podem compartilhar subgrupos próprios, e essa contagem **não vale** sem hipóteses adicionais. Por isso a ferramenta só usa o argumento quando o maior primo entre os Sylows não normais tem α = 1.

## Lógica de decisão

A função `render(n)` segue esta ordem de verificação:

| Ordem de teste | Condição sobre |G| = n | Resultado |
|---|---|---|
| 1 | n primo | **Lagrange:** G é simples. |
| 2 | n = pᵏ, k > 1 | **Lema 3.7:** G não é simples (se k = 2, G é abeliano pelo Lema 1.9). |
| 3 | n = pq | **Lema 3.4:** n_q = 1, G não é simples. |
| 4 | n = pᵅq com pᵅ < q | **Lema 3.6:** o q-Sylow é normal. |
| 5 | n = pqr | **Lema 3.5:** contagem de elementos, algum Sylow é normal. |
| 6 | demais casos | Análise geral: cartas por primo, Proposição do Índice, contagem de elementos (se válida) e conclusões estruturais. |

Na análise geral, o resumo final é:

- 🟢 **todos os Sylows são normais**, se cada primo tem nₚ = 1 como único candidato;
- 🟠 **G não é simples**, se algum Sylow é normal ou a Proposição do Índice (ou a contagem) conclui;
- ⚪ **inconclusivo**, se nenhum Sylow é necessariamente normal e nenhum dos métodos conclui.

## Exemplos

Resultados obtidos executando a própria lógica da página:

| |G| | Fatoração | Resultado |
|---|---|---|
| **12** | 2² · 3 | Contagem de elementos: o 2-Sylow é normal (único). Também pela Proposição do Índice. **Não simples.** |
| **15** | 3 · 5 | Lema 3.4. **Não simples**; todos os Sylows são normais. |
| **28** | 2² · 7 | Lema 3.6: o 7-Sylow é normal. **Não simples.** |
| **33** | 3 · 11 | Lema 3.4. **Não simples**; todos os Sylows são normais. |
| **56** | 2³ · 7 | Contagem de elementos: o 2-Sylow é normal (único). **Não simples.** |
| **63** | 3² · 7 | n₇ = 1 (7-Sylow normal); n₃ ∈ {1, 7}. **Não simples.** |
| **72** | 2³ · 3² | n₂ ∈ {1, 3, 9}, n₃ ∈ {1, 4}. Proposição do Índice aplicada aos 3-Sylows. **Não simples.** |
| **20449** | 11² · 13² | n₁₁ = n₁₃ = 1. Todos os Sylows são normais; G é **nilpotente e abeliano**. |
| **7** | 7 | Lagrange: G é **simples**. |
| **16** | 2⁴ | Lema 3.7: **não simples**. |
| **30** | 2 · 3 · 5 | Lema 3.5: **não simples**. |
| **60** | 2² · 3 · 5 | **Inconclusivo**: nenhum Sylow é necessariamente normal e os métodos não decidem. |
| **168** | 2³ · 3 · 7 | **Inconclusivo**, pelo mesmo motivo. |

As ordens **60** e **168** são justamente as ordens dos grupos simples A₅ e PSL(2,7). Quando o resultado é ⚪ inconclusivo, isso **não** significa que o grupo seja simples. Significa apenas que os argumentos automáticos não bastam e que seria necessária uma análise caso a caso.

## Estrutura do código

Tudo está em `index.html`:

| Trecho | Conteúdo |
|---|---|
| **HTML + CSS** | Campo de entrada, botões de exemplo, área de resultados e painel de referência. |
| `factorize(n)` | Fatoração por divisão sucessiva. |
| `getDivisors(n)` | Divisores de n, em ordem crescente. |
| `legendreVal(n, p)` e `orderDividesFact(G, k)` | Verificam se |G| divide k! pelas valuações de Legendre, sem calcular o fatorial. |
| `elementCountArgument` e `countingBlockedByAlpha` | Argumento de contagem de elementos e o aviso de quando ele não se aplica (α > 1). |
| `render(n)` | Aplica a lógica de decisão e monta o HTML dos resultados. |
| `runAnalysis`, `setExample`, `toggleRef` | Eventos da interface (botão Analisar, exemplos e painel de referência). |

## Limitações

- A entrada deve ser um **inteiro entre 2 e 9.999.999**.
- O resultado vale para **todo grupo da ordem informada**. A ferramenta não analisa um grupo específico.
- Os métodos automáticos (Sylow, Proposição do Índice, contagem de elementos e lemas) **não decidem todas as ordens**. Nos casos inconclusivos (como 60 e 168), a resposta correta exige outras técnicas.
- O argumento de contagem de elementos só é aplicado quando o maior primo dentre os Sylows não normais tem α = 1.
- Ferramenta com **fins didáticos**: serve para explorar e conferir raciocínios, mas não substitui a demonstração formal.

## Executando localmente

Não há instalação nem build. Baixe o arquivo e abra no navegador (funciona offline):

```bash
git clone https://github.com/lbemm3/subgrupos-de-sylow.git
cd subgrupos-de-sylow
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Ou use um servidor local:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000/
```

## Publicação via GitHub Pages

O arquivo deve se chamar `index.html` para a página abrir direto na raiz do endereço.

1. No repositório, vá em **Settings → Pages**.
2. Em *Build and deployment*, selecione **Deploy from a branch**.
3. Escolha a branch principal (`main`) e a pasta `/ (root)`, e clique em **Save**.
4. Após alguns minutos, a ferramenta estará em <https://lbemm3.github.io/subgrupos-de-sylow/>.

## Autoria e licença

Desenvolvido por **Laerte Bemm** (Álgebra Abstrata, Departamento de Matemática, Universidade Estadual de Maringá – UEM).

Licença: defina a licença do repositório (por exemplo, MIT) e inclua o arquivo `LICENSE`.
