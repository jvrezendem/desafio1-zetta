# Análise Socioecoômica e de Criminalidade em Minas Gerais

Este repositório contém o trabalho desenvolvido para o Desafio 1 do programa Zetta Lab. O objetivo é concluir como podemos avaliar e prever/visualizar os agentes/fenômenos que mais causam impactos socioeconômicos no Brasil.

# Contexto e Motivação 

O Brasil, um país de dimensões continentais e uma diversidade social, econômica e ambiental, é influenciado por múltiplos fatores e agentes que atuam de modo interligado para determinar os impactos socioeconômicos em diferentes regiões do país. A qualidade e cobertura dos serviços de saúde influenciam diretamente a expectativa de vida, o bem-estar e a produtividade; a educação repercute tanto na formação de cidadãos mais capacitados e conscientes quanto no potencial de crescimento econômico e na diminuição das desigualdades sociais. Questões ligadas à segurança pública, como violência, taxas de homicídio e criminalidade, afetam o bem-estar coletivo, a economia local e as oportunidades de desenvolvimento, especialmente em áreas urbanas e vulneráveis. Além disso, fenômenos ambientais (como desmatamento, secas, enchentes e poluição) provocam consequências econômicas e sociais significativas, afetando famílias, comunidades e setores produtivos. Fatores econômicos como desemprego, inflação e desigualdade de renda também contribuem para a instabilidade e perpetuação da pobreza e da vulnerabilidade social. Assim, avaliar e prever os agentes e fenômenos que mais causam impactos socioeconômicos no Brasil exige o uso integrado de dados multidimensionais para fundamentar políticas públicas mais eficazes, justas e voltadas às especificidades regionais e populacionais. Modelos preditivos, fundamentados em análises estatísticas e exploratórias, podem contribuir para identificar padrões, antecipar impactos, mapear regiões vulneráveis e direcionar decisões estratégicas voltadas à redução sustentável da pobreza e à promoção do desenvolvimento humano e social.

Devido a quantidade de dados a serem analisados para uma abordagem nacional, foi escolhido o **Estado de Minas Gerais** como forma de diminuir o contingente de dados e assim, aumentar o detalhamento da análise. O estado foi dividido segundo as RISPs **(Regiões Integradas de Segurança Pública)** definidas pela Polícia Militar, e para cada região foram consolidados indicadores de renda, educação, expectativa de vida e criminalidade. Assim, é possível responder à pergunta central:

**Como avaliar e visualizar os agentes/fenômenos que mais impactam o desenvolvimento socioeconômico nas diferentes regiões de Minas Gerais?**

# Escolha dos Dados

Abaixo estão listados os principais arquivos em `data/bruto` utilizados na construção da base, acompanhados de uma breve descrição e da fonte original. Cada base foi selecionada por sua relevância para representar dimensões sociais, econômicas, demográficas e de segurança pública, compondo um panorama multidimensional da realidade mineira.

| **Tabela**                      | **Descrição**                                                                                                                                                                       | **Fonte Oficial**                                                                                                                                                |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`municipios_risp.csv`**       | Relação de todos os municípios de Minas Gerais com suas respectivas RISPs (Regiões Integradas de Segurança Pública). Essa estrutura permitiu consolidar os dados em nível regional. | [Portal da Secretaria de Estado de Justiça e Segurança Pública de Minas Gerais (SEJUSP)](https://www.seguranca.mg.gov.br/index.php/integracao/unidades-integrad) |
| **`crimes_por_regiao.csv`**     | Quantitativo de crimes violentos registrados por RISP. Os dados foram filtrados e somados por região, permitindo análise espacial da criminalidade.                                 | [Dados Abertos do Governo de Minas Gerais – Crimes Violentos](https://dados.mg.gov.br/dataset/crimes-violentos/resource/b6900c69-6244-449f-bac8-771995fba5a7)    |
| **`popTotal_2022.csv`**         | População total estimada em 2022 para cada município de Minas Gerais. Utilizada para ponderar indicadores e calcular médias regionais.                                              | [IBGE via IPEA Data – Indicadores Municipais](https://www.ipeadata.gov.br/Default.aspx)                                                                          |
| **`renda_per_capita_2010.csv`** | Renda média per capita dos municípios mineiros no Censo 2010, corrigida pela inflação acumulada até 2025 para comparabilidade econômica.                                            | [IBGE / IPEA Data](https://www.ipeadata.gov.br/Default.aspx)                                                                                                     |
| **`taxa_analfabetismo.csv`**    | Taxa de analfabetismo da população com 15 anos ou mais, por município, utilizada para estimar níveis de escolarização e exclusão educacional.                                       | [IBGE / IPEA Data](https://www.ipeadata.gov.br/Default.aspx)                                                                                                     |
| **`esperanca_vida.csv`**        | Expectativa de vida média por município, utilizada como proxy de qualidade de vida e acesso à saúde.                                                                                | [IBGE / IPEA Data](https://www.ipeadata.gov.br/Default.aspx)                                                                                                     |

Os dados municipais foram escolhidos por sua abrangência e detalhamento, permitindo consolidar informações em nível de RISP.

A integração entre variáveis socioeconômicas e de segurança pública viabilizou uma análise exploratória capaz de revelar relações estruturais entre desenvolvimento humano e criminalidade.

As fontes (SEJUSP, IPEA e IBGE) foram priorizadas por serem oficiais, abertas e atualizadas, garantindo credibilidade e reprodutibilidade científica ao estudo.

A divisão do estado de Minas Gerais em **Regiões Integradas de Segurança Pública (RISPs)** foi adotada para **garantir uma análise territorial mais precisa e coerente com a estrutura operacional da segurança pública estadual.**
Enquanto as divisões administrativas tradicionais (como mesorregiões ou microrregiões) refletem critérios geográficos e econômicos, as RISPs representam **delimitações criadas pela Polícia Militar e pela Secretaria de Segurança Pública com base em características populacionais, econômicas e criminais reais**.
Essa abordagem permite **integrar dados de diferentes naturezas (socioeconômica, demográfica e criminal)** dentro de uma mesma unidade regional de gestão da segurança, facilitando a identificação de **padrões locais de vulnerabilidade e desenvolvimento**.
Dessa forma, o estudo não apenas descreve o estado de forma estatística, mas também fornece **informações práticas e aplicáveis ao planejamento de políticas públicas, tornando a análise mais relevante e alinhada ao contexto institucional de Minas Gerais**.

# Banco Processado 

Os dados brutos foram combinados e agregados, resultando em uma base final armazenada em `data/processado/database_rispMG.csv`. Cada linha representa uma RISP (total de 19 regiões) e contém os seguintes campos:

| Coluna                     | Descrição                                                                             |
| -------------------------- | ------------------------------------------------------------------------------------- |
| `risp`                     | Identificador numérico da região integrada de segurança pública.                      |
| `total_crimes`             | Total de crimes violentos registrados na RISP no período analisado.                   |
| `latitude`, `longitude`    | Coordenadas médias aproximadas da RISP para fins de mapa.                             |
| `populacao`                | População total da RISP (soma das populações municipais).                             |
| `renda_media`              | Renda per capita média (corrigida para 2025) ponderada pela população dos municípios. |
| `idh_medio`                | Índice de Desenvolvimento Humano médio dos municípios da RISP.                        |
| `taxa_de_analfabetismo(%)` | Taxa média de analfabetismo da população (≥ 15 anos) na RISP.                         |
| `esperanca_vida`           | Expectativa de vida média da RISP.                                                    |

### Visualização do Banco de Dados Final

| RISP | Total de Crimes | População | Renda Média | IDH Médio | Taxa de Analfabetismo (%) | Esperança de Vida |
|------|----------------:|-----------:|--------------:|-----------:|---------------------------:|-------------------:|
| 1 | 7.800 | 1.118.836 | 1.361.68 | 0.738 | 7.37 | 75.67 |
| 2 | 2.889 | 1.906.359 | 1.005.22 | 0.695 | 8.38 | 75.29 |
| 3 | 4.134 | 1.574.197 | 1.150.62 | 0.673 | 9.44 | 74.83 |
| ... | ... | ... | ... | ... | ... | ... |

# Metodologia 

A construção do banco de dados e da análise exploratória seguiu as etapas resumidas abaixo:

1. **Coleta e integração de dados brutos** – os arquivos originais encontram‑se em data/bruto/. Eles trazem informações sobre população, renda per capita, escolarização por gênero, taxa de analfabetismo, expectativa de vida e delitos registrados por município. Essas tabelas foram obtidas de bases públicas (PMMG, IBGE/IPEA e governo de Minas Gerais).

1. **Limpeza e padronização** – as colunas foram normalizadas (espaços removidos), valores ausentes foram tratados e números com separador decimal em vírgula foram convertidos para ponto. Algumas séries históricas (como renda de 2010) foram corrigidas para valores atuais usando o IPCA acumulado até 2025.

1. **Relacionamento das tabelas** – todos os conjuntos foram associados por município. A relação município–RISP (`municipios_risp.csv`) permitiu agrupar os dados por região. Em seguida os valores foram agregados:

- **População**: soma da população dos municípios por RISP.

- **Renda média per capita (corrigida)**: média simples.

- **Taxa de analfabetismo e esperança de vida**: médias ponderadas.

- **Total de crimes**: soma dos registros de crimes violentos por RISP.

1. Análise exploratória e visualizações – com a base final consolidada, foram calculadas correlações entre os indicadores e produzidos gráficos de dispersão e mapas. As principais relações observadas foram: renda média e IDH correlacionados positivamente; taxa de analfabetismo correlacionada negativamente com IDH; regiões com pior desenvolvimento humano concentrando mais crimes; taxa de analfabetismo correlacionada positivamente com o número de crimes; e esperança de vida e IDH correlacionados positivamente.

1. Ferramentas utilizadas –

- **Pandas** para manipulação e agregação das tabelas;

- **Matplotlib** para construção de gráficos (correlação, dispersões);

- **Folium** para visualizações geográficas interativas (mapas de calor das RISPs).

# Visualizações

Algumas das visualizações produzidas durante a análise exploratória estão disponíveis na pasta `assets/` e são referenciadas abaixo:

<p align="center">
  <img src="https://github.com/jvrezendem/desafio1-zetta/blob/main/assets/heatMap_Indicadores.png?raw=true" />
</p>

A matriz de correlação evidencia relações importantes: 
- Quando o **IHD (Índice de Desenvolvimento Humano)** aumenta, o **número de crimes violentos** diminui, a **renda média** é maior, a **taxa de analfabetismo** é menor e a **esperança de vida é maior**.

- O número de crimes violentos em uma região é um indicador de outros problemas, uma vez que, quando ele aumenta, o **IDH** diminui, a **renda média** da região diminui, a **esperança de vida** diminui e a **taxa de analfabetismo** aumenta.

Os mapas mostram a distribuição espacial das RISPs em Minas Gerais. O tamanho dos marcadores é proporcional ao número de crimes violentos registrados em cada região; observa‑se que as maiores concentrações de criminalidade se encontram em algumas áreas específicas, indicando possível relação com fatores socioeconômicos.

🔗 [Clique aqui para abrir o mapa de calor interativo](../src/msp1/mspa_calor_crimes_MG.html)

Legenda:

| Cor             | Critério                                              | Interpretação                                                                                                              |
| --------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 🔴 **Vermelho** | RISP com **maior número de crimes**  | Regiões **mais críticas**, onde há **maior incidência criminal** e, possivelmente, **piores indicadores socioeconômicos**. |
| 🔵 **Azul**    | RISP com **menor número de crimes** | Regiões **mais estáveis ou seguras**, geralmente com **melhores índices de renda, IDH e educação**.                        |


🔗 [Clique aqui para abrir o mapa de regiões criticas interativo](../src/msp2/mspa_criminalidade.html)

Legenda:

| Cor             | Critério                                              | Interpretação                                                                                                              |
| --------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 🔴 **Vermelho** | RISP com **total de crimes acima da média estadual**  | Regiões **mais críticas**, onde há **maior incidência criminal** e, possivelmente, **piores indicadores socioeconômicos**. |
| 🟢 **Verde**    | RISP com **total de crimes abaixo da média estadual** | Regiões **mais estáveis ou seguras**, geralmente com **melhores índices de renda, IDH e educação**.                        |
