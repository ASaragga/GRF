# GRF - Gestão de Riscos Financeiros
![](GRF01.jpg?raw=true)

- Medindo o Risco de Perda: VaR e ETL
- Mercado de Ações
- Mercado Cambial
- Risco de Taxa de Juro
- Risco de Crédito

## Guia de Instalação e Desenvolvimento Julia
### Instalação do Julia

1 Transferir Julia

2 Visite o website oficial da linguagem Julia: https://julialang.org/downloads/

3 Escolha a versão adequada para o seu sistema operativo (Windows, macOS ou Linux)

4 Transfira a versão estável mais recente

### Gestão de Pacotes

Pacote das disciplinas GRF e ARE: Valorização, Aquisição e Reorganização de Empresas (VARe). VARe também referencia a medida de risco de perda: VaR

Instalar Pacote VARe.jl a partir do Repositório no GitHub
```
using Pkg
Pkg.add("https://github.com/ASARAGGA/VARe.jl")
```
Instalar Pacotes do Repositório Oficial
```
using Pkg
Pkg.add("Distributions")

```
Neste caso estamos a instalar o pacote `Distributions` que dá acesso a um grande número de distribuições de probabilidade incluindo a Normal e a T-Student.
A instalação de pactores apenas necessita de ser feita uma vez. 

Antes de os pacotes instalados poderem ser utilizados numa sessão teremos recorrer ao comando: `using`, como no seguinte exemplo,
```
using VARe
p = get_prices("IBM",Date(2025,02,01), Date(2025,03,03))
println(DataFrame(p))
```
Neste caso, utilizamos a função `get_prices` para extrair a partir do Yahoo Finance as cotações das ações da IBM para o período compreendidon entre 1 de Fevereiro e 3 de Março de 2025. `DataFrame` organiza os dados numa tabela e `println` imprime a informação recolhida. Aqui `adjclose` representa as cotações de fecho ajustadas por emissão de novas ações, pagamento de dividendos, stock splits e reverse splits.
```
19×8 DataFrame
 Row │ ticker  timestamp            open     high     low      close    adjclose  vol       
     │ String  DateTime             Float64  Float64  Float64  Float64  Float64   Float64   
─────┼──────────────────────────────────────────────────────────────────────────────────────
   1 │ IBM     2025-02-03T14:30:00  250.73   260.326  250.173   260.73   259.004  8.35285e6
   2 │ IBM     2025-02-04T14:30:00  258.279  263.495  256.412   264.46   262.71   6.03748e6
   3 │ IBM     2025-02-05T14:30:00  263.951  263.961  259.451   263.3    261.557  6.1243e6
   4 │ IBM     2025-02-06T14:30:00  261.24   261.637  251.057   253.44   251.763  6.08774e6
   5 │ IBM     2025-02-07T14:30:00  253.591  255.23   250.352   252.34   250.67   3.34799e6
   6 │ IBM     2025-02-10T14:30:00  250.86   251.95   246.87    249.27   249.27   3.5644e6
   7 │ IBM     2025-02-11T14:30:00  251.1    256.75   250.58    254.7    254.7    4.8016e6
   8 │ IBM     2025-02-12T14:30:00  252.72   256.4    252.02    255.81   255.81   3.0753e6
   9 │ IBM     2025-02-13T14:30:00  255.66   259.28   254.41    259.19   259.19   4.5315e6
  10 │ IBM     2025-02-14T14:30:00  259.0    261.94   257.91    261.28   261.28   3.9253e6
  11 │ IBM     2025-02-18T14:30:00  261.93   263.96   259.83    263.07   263.07   4.2628e6
  12 │ IBM     2025-02-19T14:30:00  262.0    264.36   260.09    264.32   264.32   3.7187e6
  13 │ IBM     2025-02-20T14:30:00  263.65   265.09   262.15    264.74   264.74   4.8848e6
  14 │ IBM     2025-02-21T14:30:00  263.85   264.83   261.1     261.48   261.48   5.6679e6
  15 │ IBM     2025-02-24T14:30:00  261.5    263.85   259.58    261.87   261.87   4.3981e6
  16 │ IBM     2025-02-25T14:30:00  261.08   263.48   256.77    257.75   257.75   6.2922e6
  17 │ IBM     2025-02-26T14:30:00  258.1    258.33   254.41    255.84   255.84   3.4601e6
  18 │ IBM     2025-02-27T14:30:00  255.22   257.63   253.05    253.23   253.23   3.4022e6
  19 │ IBM     2025-02-28T14:30:00  250.86   252.81   246.54    252.44   252.44   7.9888e6
```
Podemos também obter informação intra-diária, adicionado o argumento da função relativo ao intervalo desejado entre cotações, para trinta minutos: "30m". Por omissão, a função `get_prices` considera o período de 1 dia: "1d", não sendo pois necessário neste caso incluir o argumento relativo ao intervalo entre cotações.
```
q = get_prices("IBM",DateTime(2025,02,26,0,0,0), DateTime(2025,02,26,23,59,59), interval = "30m")
q = DataFrame(q)
@show q
```
Agora utilizámos o macro `@show` em vez da função `println`,
```
DataFrame(q) = 14×7 DataFrame
 Row │ ticker  timestamp            open     high     low      close    vol
     │ String  DateTime             Float64  Float64  Float64  Float64  Float64
─────┼───────────────────────────────────────────────────────────────────────────
   1 │ IBM     2025-02-26T14:30:00  258.1    258.325  254.725  257.15   410371.0
   2 │ IBM     2025-02-26T15:00:00  257.37   257.63   256.743  257.09   200261.0
   3 │ IBM     2025-02-26T15:30:00  257.06   258.31   257.06   257.58   175166.0
   4 │ IBM     2025-02-26T16:00:00  257.63   257.82   256.69   257.135  159783.0
   5 │ IBM     2025-02-26T16:30:00  257.185  257.815  256.8    257.18   169407.0
   6 │ IBM     2025-02-26T17:00:00  257.22   257.55   256.5    256.78   136203.0
   7 │ IBM     2025-02-26T17:30:00  256.86   256.96   255.05   255.265  171722.0
   8 │ IBM     2025-02-26T18:00:00  255.24   255.6    254.72   254.75   192352.0
   9 │ IBM     2025-02-26T18:30:00  254.775  255.37   254.48   254.76   170643.0
  10 │ IBM     2025-02-26T19:00:00  254.76   256.07   254.41   255.945  228415.0
  11 │ IBM     2025-02-26T19:30:00  255.945  256.99   255.84   255.84   204101.0
  12 │ IBM     2025-02-26T20:00:00  255.81   256.2    255.55   255.89   171285.0
  13 │ IBM     2025-02-26T20:30:00  255.83   257.01   255.53   255.85   497780.0

```
Podemos agora extrair as cotações da coluna `close` do DataFrame para um vetor (o qual lhe podemos chamar por exemplo `fim30m`) e com base nelas, calcular a média e o devio-padrão.
```
using Statistics

fim30m = q[:,6]         # fim30m é um vetor com todos os elementos da 6ª coluna (close) do DataFrame
@show mean(fim30m)
@show std(fim30m)
```
Necessitamos de declarar `using Statistics` para calcular a média e o desvio-padrão. Normalmente esta declaraçoes são colocadas no iníco de cada script
```
mean(fim_periodo) = 256.03035627092635
std(fim_periodo) = 1.233216189409658
```















