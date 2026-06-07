# Conferência Automática Lotofácil

#### Análise de Apostas por Ano

Conferidor visual e inteligente para jogos da Lotofácil. Você informa **15 dezenas** e um **ano**, e o app percorre **todos os concursos daquele ano**, conta quantos pontos a sua aposta faria em cada sorteio e mostra os prêmios das apostas premiadas (11 a 15 acertos), com totais.

A partir da **versão 8**, o app também sabe **guardar os resultados num arquivo de texto (TXT)** e **lê-lo de volta** — assim as próximas consultas ficam **instantâneas e offline**, sem precisar baixar tudo de novo.

## Novidades da versão 8 (resumo)

* 🗂️ **Cache local inteligente** — concursos já consultados ficam guardados na memória; o app só baixa o que ainda falta.
* ⬇️ **Relatório anual em TXT** — exporta as 15 dezenas de **cada** concurso do ano + os prêmios por faixa.
* ⬆️ **Importação do relatório** — recarregue o TXT e as consultas daquele ano passam a ser **offline / instantâneas**.
* 🟢 **Indicador de cache** — um selo mostra quantos concursos estão guardados e se o ano está completo.
* 🐞 **Correções** — rodapé com cores corrigidas e fim da “piscada” da tabela ao calcular prêmios.

> **Por que isso importa?** Um sorteio já realizado **nunca muda** — é um fato imutável. Sem cache, cada clique refazia centenas de requisições pela internet para buscar dados que você já tinha. O relatório TXT transforma esse trabalho repetido em **uma consulta única**, que você guarda e reaproveita.

## Recursos

**Conferência (já existia):**

* Quantas vezes a sua aposta seria premiada no ano (de 11 a 15 acertos)
* 1 aposta de 15 dezenas por consulta
* Conferência automática de todos os concursos do ano
* Destaque para prêmios e valores de premiação
* Tabela com concurso, data, acertos e prêmio
* Quantidade de concursos no ano
* Quantidade de apostas premiadas
* Total ganho no ano
* Interface responsiva (funciona no celular)

**Cache e relatório (novo na v8):**

* Exportação do relatório anual em **TXT** (15 dezenas de cada concurso + prêmios por faixa)
* Importação do relatório para **consultas offline e instantâneas**
* Cache local que **baixa apenas os concursos que faltam**
* Selo de status do cache (✓ ano completo · ~ parcial) com botão **limpar**

## Como usar — conferência básica

1. **Insira 15 dezenas** (de 1 a 25). Vale separar por vírgula ou espaço — por exemplo `1, 7, 11, 15...` ou `1 7 11 15...`.
2. **Selecione o ano** que você quer analisar (a Lotofácil existe desde 2003).
3. **Clique em “▶ Verificar Sorteios”** e aguarde.

O app mostra, numa tabela, todos os concursos em que a sua aposta teria feito **11 acertos ou mais**, com o prêmio de cada um e os totais do ano no rodapé.

## Novidades da versão 8 — passo a passo (didático)

Esta seção explica, com calma, **como usar o cache e o relatório TXT** e **o que acontece por trás**.

### 1) Gerar (baixar) o relatório do ano

1. Digite o **ano** desejado (não precisa preencher as dezenas — o relatório é sobre os **sorteios**, não sobre o seu jogo).
2. Clique em **“⬇ Baixar relatório do ano (TXT)”**.
3. O app baixa os concursos que faltam, monta o arquivo e salva como **`Lotofacil-AAAA.txt`** (ex.: `Lotofacil-2024.txt`).

Esse arquivo é **independente da sua aposta**: ele guarda só os sorteios, então serve para conferir **qualquer** jogo naquele ano, hoje ou no futuro.

### 2) Carregar (importar) um relatório

1. Clique em **“⬆ Carregar relatório (TXT)”**.
2. Escolha o arquivo `Lotofacil-AAAA.txt` que você salvou antes.
3. Pronto — o app preenche o ano automaticamente e o selo de cache aparece. A partir daí, **conferir aquele ano é instantâneo**.

### 3) O que acontece nos bastidores

Toda consulta passa por uma única “porta de entrada” que escolhe o caminho **mais barato**:

* **Ano já fechado e completo no cache → nenhuma requisição.** A resposta é imediata, sem internet.
* **Ano corrente (em andamento) →** o app busca só o **último concurso** e completa apenas os sorteios mais recentes que faltam.
* **Caso geral →** descobre o primeiro e o último concurso do ano e baixa **somente os buracos**, nunca o ano inteiro de novo.

### 4) O selo (badge) do cache

Logo abaixo dos botões aparece um selo verde com o estado atual, por exemplo:

Cache local — 312 concurso(s)  [ 2023: 156✓  ·  2024: 156~ ]   (✓ completo · ~ parcial)

* **✓** = aquele ano está **completo** (dá para consultar offline).
* **~** = aquele ano está **parcial** (faltam concursos; a próxima consulta baixa o que falta).
* O botão **“limpar”** esvazia o cache, caso você queira começar do zero.


## Formato do arquivo TXT (como ler e editar)

O relatório foi feito para ser **legível por você** e, ao mesmo tempo, **fácil de o app reler**. Veja um exemplo real:

```
# ============================================================
#  RELATÓRIO LOTOFÁCIL — ANO 2024
#  Gerado pelo Verificador Lotofácil em 02/06/2026
#  As 15 dezenas sorteadas de cada concurso + prêmio por faixa.
# ============================================================
@META ano=2024 primeiro=3001 ultimo=3003 completo=sim gerado=02/06/2026 total=3

3001 | 05/01/2024 | 01-02-03-04-05-06-07-08-09-10-11-12-13-14-15 | 15:ACUM 14:1.500,50 13:30,00 12:12,00 11:6,00
3002 | 08/01/2024 | 02-04-06-08-10-12-14-16-18-20-22-24-01-03-05 | 15:1.234.567,89 14:2.000,00 13:30,00 12:10,00 11:5,00
```

### Cada linha de dados tem 4 partes, separadas por `|`

| Parte | Conteúdo | Exemplo |
|------|----------|---------|
| 1 | Número do concurso | `3001` |
| 2 | Data da apuração (DD/MM/AAAA) | `05/01/2024` |
| 3 | As 15 dezenas sorteadas | `01-02-...-15` |
| 4 | Prêmios por faixa de acerto | `15:ACUM 14:1.500,50 ...` |

### Como ler os prêmios (parte 4)

Cada item é `acertos:valor`, sempre na ordem **15 → 11**:

| Token | Significado |
|-------|-------------|
| `14:1.500,50` | Prêmio **por ganhador** de quem fez 14 pontos: R$ 1.500,50 |
| `15:ACUM` | A faixa **acumulou** (ninguém acertou; prêmio passou ao próximo concurso) |
| `13:?` | Valor **desconhecido** (a fonte não informou esse prêmio) |

### As linhas especiais

* **Linhas que começam com `#`** são **comentários**: explicações para você. Pode editar ou apagar à vontade — o app as ignora.
* **A linha `@META`** guarda os metadados do relatório:
  * `ano`, `primeiro` e `ultimo` — o ano e a faixa de concursos cobertos;
  * `completo=sim|parcial` — se o ano está inteiro;
  * `gerado` — a data em que o arquivo foi criado;
  * `total` — quantos concursos o arquivo contém.

> 💡 Você pode até montar um TXT **à mão** (ou colar dados de outra fonte). Desde que cada linha siga `concurso | data | 15 dezenas | prêmios`, o app aceita. Linhas mal formatadas são simplesmente ignoradas, sem quebrar a importação.

## Garantias e limitações (em bom português)

* **“Completo” é confiável.** O app só grava `completo=sim` quando o ano **já estava encerrado** no momento da geração **e** todos os concursos estão presentes, sem buracos. Um retrato tirado no meio do ano corrente nunca é marcado como completo — fica `parcial`. Por isso a consulta offline nunca te entrega um ano “pela metade” achando que está inteiro.
* **Autocorreção.** Se você reabrir, no ano seguinte, um relatório do ano corrente gerado hoje, o app confirma o final do ano com pouquíssimas requisições e **promove** aquele ano a “completo” sozinho.
* **Limitação honesta dos prêmios `?`.** Se um relatório de ano fechado tiver prêmios marcados como `?`, a consulta totalmente offline **não** vai sair para buscá-los, e eles aparecerão como **EST** (estimado/indisponível). Na prática isso é raro: a API da Caixa devolve todas as faixas de uma vez, então arquivos gerados pelo próprio app quase sempre já trazem todos os valores.

## Perguntas frequentes

**O cache fica salvo quando eu fecho o navegador?**
Não. O cache vive **na memória da aba** e some ao recarregar. É exatamente por isso que existe o relatório TXT: ele é a sua “memória permanente”. Para ter consultas offline numa nova sessão, basta **carregar o TXT** de novo.

**Posso compartilhar o arquivo TXT com outra pessoa?**
Sim. Ele é um texto comum, portátil. Qualquer pessoa com o app pode importá-lo e consultar o mesmo ano instantaneamente.

**Preciso de internet?**
Na **primeira** vez sim — para baixar os concursos do ano. Depois, para um **ano fechado e completo**, **não**: a conferência roda 100% offline a partir do cache/relatório.

**O “Total ganho no ano” é o meu lucro?**
Não. Esse valor é o **total bruto** dos prêmios. Ele **não desconta** o custo de ter apostado em todos os concursos (cada aposta de 15 dezenas tem um preço, multiplicado pela quantidade de concursos do ano). Trate o número como “quanto sairia em prêmios”, não como lucro líquido.

**Por que o app usa vários endereços (proxies) para acessar a Caixa?**
A API da Caixa não libera acesso direto pelo navegador (bloqueio de CORS), então o app tenta várias rotas públicas. Elas podem ficar instáveis — e é mais um motivo para o cache: depois que o ano está guardado, você deixa de depender dessas rotas.

## Como funciona por dentro (para curiosos e desenvolvedores)

* **Arquivo único** HTML + CSS + JavaScript (sem dependências, sem build).
* **Fonte de dados:** API oficial da Caixa, acessada via rotas (proxies) CORS.
* **Camada de cache (v8):**
  * `DRAW_CACHE` — guarda cada concurso já baixado no formato nativo da Caixa;
  * `YEAR_COVERAGE` — registra, por ano, o primeiro/último concurso e se está completo;
  * `ensureYearCached(ano)` — a “porta de entrada” única que decide entre **zero requisições** (ano completo no cache), **completar só o que falta** ou **mapear e baixar os buracos**.
* **Relatório TXT:** funções de **serialização** (montar o arquivo) e **leitura tolerante** (reconstruir os concursos e os prêmios por faixa, ignorando comentários e linhas inválidas).

## Requisitos

* Um navegador moderno (Chrome, Edge, Firefox, Safari).
* Conexão com a internet **na primeira consulta** de cada ano. Depois, anos completos funcionam offline.

## Aviso

Este app é uma ferramenta de **conferência e estudo**. Loteria é um jogo de azar — jogue com responsabilidade e dentro do seu orçamento.

## Autor

**Janer Dorneles**

*Versão 8 — cache local + relatório TXT (consultas offline e instantâneas).*

https://janerdorneles.github.io/Lotofacil-Ano/
