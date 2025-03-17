# GRF - Gestão de Riscos Financeiros
![](GRF01.jpg?raw=true)

- Medindo o Risco de Perda
   - Notebook 01: VaR
      - [Google Colab](https://colab.research.google.com/github/ASaragga/GRF/blob/main/VaR.ipynb) (dinâmico)
      - [GitHub](https://github.com/ASaragga/GRF/blob/main/VaR.ipynb) (estático)
   - Notebook 02: ETL
   - Notebook 02: Abordagens Paraméticas, Simulação Histórica e Simulação de Monte-Carlo
   - Notebook 03: Risco de Perda em Carteiras de Grande Dimensão
- Mercado de Ações
- Mercado Cambial
- Risco de Taxa de Juro
- Risco de Crédito

# 1 - Guia de Instalação e Desenvolvimento Julia

## 1.1 - Instalação do Julia

1 Transferir Julia

2 Visite o website oficial da linguagem Julia: https://julialang.org/downloads/

3 Escolha a versão adequada para o seu sistema operativo (Windows, macOS ou Linux)

4 Transfira a versão estável mais recente

## 1.2 - Gestão de Bibliotecas

Biblioteca das disciplinas GRF e ARE: Caramel.jl

### 1.2.1 - Instalação Local da Biblioteca Caramel.jl
Na nossa aplicação Julia local, instalamos a biblioteca Caramel.jl a partir do Repositório no GitHub,
```
using Pkg
Pkg.add(url="https://github.com/ASaragga/Caramel.jl")
```
Esta instalação apenas necessita de ser feita uma vez.

### 1.2.2 - Instalação Online da Biblioteca `Caramel.jl` no Google Colab
Primeiro, no início de cada sessão, teremos sempre que alterar o runtime do Google Colab de Python para Julia. Pois, por omissão, o runtime do Google Colab  é definido inicialmente como sendo Python.

<p align="center">
  <img src="ColabRuntime.png?raw=true" alt="Colab Runtime" width="700">
</p>

Uma vez definido o runtime como Julia, para fazer a instalação do Caramel no Google Colab,

<p align="center">
  <img src="GoogleColab.png?raw=true" alt="Instalação Caramel" width="700">
</p>

Esta instalação tem de ser sempre feita no início de cada sessão, pois o Google Colab não persiste as bibliotecas instaladas entre sessões. A instalação de bibliotecas do repositório oficial processa-se de uma forma um pouco mais simples,
```
using Pkg
Pkg.add("Turing")
```
Antes de os pacotes instalados poderem ser utilizados numa sessão, teremos de recorrer ao comando: `using`, como no seguinte exemplo,
```
using Caramel

p = AssetPrice("IBM",Date(2025,02,01), Date(2025,03,03))
println(DataFrame(p))
```
Utilizamos a função AssetPrice para extrair a partir do website Yahoo Finance as cotações das ações da IBM para o período compreendido entre 1 de Fevereiro e 3 de Março de 2025. DataFrame organiza os dados numa tabela e `println` imprime a informação recolhida. A coluna :adjclose apresenta o histórico das cotações de fecho das sessões diárias da New York Stock Exchange, ajustadas por emissão de novas ações, pagamento de dividendos, stock splits e reverse splits ocorridos ao longo do tempo.















