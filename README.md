# Desaparecimento de Pessoas no Distrito Federal — Análise por Idade e Sexo (2017–2021)
Projeto final da disciplina **Introdução à Ciência de Dados**.

## Integrantes

| Nome completo | Email institucional | GitHub|
|---|---|---|
| Davi Reis Borges | davi.borges@sempreceub.com | [@DR1807](https://github.com/DR1807) |
| Gustavo Lisboa Gonçalves | gustavo.lg@sempreceub.com | [@Gustavolg95](https://github.com/Gustavolg95) |
| Rafael Guimaraens Souza | rafaguimaraens@sempreceub.com | [@RafaelGuimaraens](https://github.com/RafaelGuimaraens)|
| Marcos do Nascimento Alvarez | marcos.alvarez@sempreceub.com | [@MarcosAlvarez7](https://github.com/MarcosAlvarez7)|

## Tema

O perfil de pessoas desaparecidas no Distrito Federal entre 2017 e 2021, observado por **faixa etária** e **sexo**.

## Pergunta orientadora

**Pergunta principal:** Como o perfil de pessoas desaparecidas no Distrito Federal evoluiu entre 2017 e 2021, considerando faixa etária e sexo — e quais grupos apresentam padrões mais persistentes ou mais sujeitos a variações ao longo do período?

**Perguntas secundárias:**
1. A disparidade de sexo na faixa de 12 a 17 anos se manteve consistente ao longo dos cinco anos, ou houve alguma inflexão?
2. A queda do total de casos (2017–2020) está distribuída igualmente entre as faixas etárias ou concentrada em algum grupo específico?
3. A proporção de homens desaparecidos cresceu de 56% (2017) para 64% (2021). Em quais faixas etárias esse crescimento é mais expressivo?

## Conjunto de dados

- **Nome:** Desaparecimento de Pessoas por Idade e Sexo — Jan/Dez de 2017 a 2021
- **Fonte:** Secretaria de Segurança Pública do Distrito Federal (SSPDF), via Banco Millenium/COOAFESP
- **Link de acesso:** [https://www.dados.df.gov.br/dataset/por-regiao-administrativa/resource/53b24562-a766-462e-addc-6313fa66cd6d](https://www.dados.df.gov.br/dataset#/por-regiao-administrativa)
- **Formato original:** CSV com 5 tabelas anuais empilhadas (2017–2021), cada uma com 7 faixas etárias (+ linha "Total") e 7 colunas (faixa etária, total, % participação, masculino, % masculino, feminino, % feminino).
- **Volume:** ≈ 13.434 casos registrados no período, condensados em 35 linhas *tidy* (5 anos × 7 faixas) após o tratamento.

## Estrutura do repositório

```
.
├── README.md                                          
├── desaparecimento-de-pessoasidade-e-sexojandez-20172021.csv    # dado bruto (fonte original)
├── Analise_Pessoas_Desaparecidas_DF_ProjetoFinal.ipynb          # notebook completo (EDA, limpeza, gráficos, conclusões)
└── projeto_final_desaparecidos_slides.pdf                       # apresentação de slides exportada em PDF
```

## Como rodar o notebook

1. Clone o repositório:
   ```bash
   git clone <url-do-repositorio>
   cd <pasta-do-repositorio>
   ```
2. Crie um ambiente e instale as dependências:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
3. Abra o notebook `Analise_Pessoas_Desaparecidas_DF_ProjetoFinal.ipynb` no Jupyter ou no Google Colab.
4. Garanta que o arquivo `desaparecimento-de-pessoasidade-e-sexojandez-20172021.csv` esteja na mesma pasta do notebook (no Colab, a primeira célula de carregamento solicita o upload do CSV, caso ele não seja encontrado).
5. Execute as células em ordem (`Run All`). O notebook não depende de nenhum dado externo além desse CSV.

## Etapas da análise

### 1. Entendimento e descrição do conjunto de dados
O CSV bruto traz 5 blocos anuais empilhados, cada um com cabeçalho próprio. Uma função de *parsing* identifica o ano de cada bloco e converte tudo em um único `DataFrame` tidy (ano × faixa etária), com cada coluna documentada quanto ao tipo (temporal, categórica ou numérica).

### 2. Completude e limpeza dos dados
- **Completude:** sem valores nulos após o parsing; "Não informado" (~1%/ano) é categoria de negócio, não dado ausente.
- **Limpeza:** a linha "Total" de cada ano foi separada em `df_totais` (é subtotal, não faixa etária); nomes de faixas padronizados.
- **Consistência:** valores convertidos de texto para `int`/`float`; checagens confirmadas (`masculino + feminino == total`; soma das faixas = "Total" do ano).

### 3. Análise e visualização (6 gráficos)
1. **Total por ano** — queda de 2017 a 2020, leve recuperação em 2021.
2. **Evolução por faixa etária** — queda concentrada em 12–17 anos (-58%).
3. **Composição etária por ano** — perfil dos desaparecidos envelhecendo.
4. **Proporção de sexo no total geral** — masculinização contínua (56% → 64%).
5. **Sexo na faixa 12–17 anos** — maioria feminina estável (66–69%).
6. **Variação da proporção masculina por faixa** — masculinização puxada pelas faixas adultas (18–50 anos).

### 4. Conclusões
1. A queda geral (2017–2020) é puxada quase só pela faixa de 12 a 17 anos.
2. A disparidade de sexo entre 12 e 17 anos (maioria feminina) é o padrão mais estável da série.
3. O aumento da proporção masculina (56% → 64%) vem das faixas adultas (18–50 anos).

**Limitação:** dados agregados, sem registros individuais — não é possível cruzar faixa etária, sexo e desfecho do caso, nem analisar por região administrativa.
