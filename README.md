# Ministerio publico do estado de Roraima (MPRR)

Este coletor tem como objetivo a recuperação de informações sobre folhas de pagamentos dos membros ativos do Ministério Público do estado de Roraima. O site com as informações pode ser acessado **[aqui](https://www.mprr.mp.br/web/transparencia/opcoesvencimentos)**.

O coletor será estruturado como uma CLI. Uma vez passado como argumentos mês e ano, será feito o download de planilhas, nos formato ODS, sendo cada uma referente a uma dessas categorias:

Folha de remuneração: Membros Ativos - As planilhas deste tipo, seguem o seguinte formato:
|Campo|Descrição|
|-----|---------|
|**Matrícula (String)**| Matrícula do funcionário.|
|**Nome (String)**| Nome completo do funcionário.|
|**Cargo (String)**| Cargo do funcionário dentro do MP.|
|**Lotação (String)**| Local (cidade, departamento, promotoria) em que o funcionário trabalha.|
|**Remuneração Básica do Cargo Efetivo (Number)**| Vencimento, GAMPU, V.P.I, Adicionais de Qualificação, G.A.E e G.A.S, além de outras desta natureza.|
|**Outras Verbas Remuneratórias, Legais ou Judiciais (Number)**|  V.P.N.I., Adicional por tempo de serviço, quintos, décimos e vantagens decorrentes de sentença judicial ou extensão administrativa.|
|**Função de Confiança ou Cargo em Comissão (Number)**| Rubricas que representam a retribuição paga pelo exercício de função (servidor efetivo) ou remuneração de cargo em comissão (servidor sem vínculo ou requisitado).|
|**Gratificação Natalina (Number)**|  Parcelas da Gratificação Natalina (13º) pagas no mês corrente, ou no caso de vacância ou exoneração do servidor.|
|**Férias Constitucionais (Number)**| Adicional correspondente a 1/3 (um terço) da remuneração, pago a membros e servidores por ocasião das férias.|
|**Abono de Permanência (Number)**| Valor equivalente ao da contribuição previdenciária, devido ao Membro/Servidor que esteja em condição de aposentar-se, mas que optou por continuar em atividade (instituído pela Emenda Constitucional nº 41, de 16 de dezembro de 2003).|
|**Contribuição Previdenciária (Number)**| Contribuição Previdenciária Oficial (Plano de Seguridade Social do Servidor Público e Regime Geral de Previdência Social).|
|**Imposto de Renda (Number)**| Imposto de Renda Retido na Fonte.|
|**Retenção por Teto Constitucional (Number)**| Valor deduzido da remuneração básica bruta, quando esta ultrapassa o teto constitucional, nos termos da legislação correspondente.|

Planilha de verbas indenizatórias e outras remunerações temporárias. Seguem o seguinte formato:

|Campo|Descrição|
|-----|---------|
|**Matrícula (String)** | Matrícula do funcionário.|
|**Nome (String)** | Nome completo do funcionário.|
|**Cargo (String)** | Cargo do funcionário dentro do MP.|
|**Lotação (String)** | Local (cidade, departamento, promotoria) em que o funcionário trabalha.|
|**Verbas Indenizatórias (Number)** | Auxílio-alimentação, Auxílio-transporte, Auxílio-Moradia, Ajuda de Custo e Abono Pecuniário|
|**Outras Remunerações Temporárias (Number)** | Substituição de função |

## Como usar

### Executando com Docker

 - Inicialmente é preciso instalar o [Docker](https://docs.docker.com/install/). 

 - Construção da imagem:

    ```sh
    $ cd coletores/mprr
    $ sudo docker build -t mprr .
    ```
 - Execução:
 
    ```sh
    $ sudo docker run -e YEAR=2020 -e MONTH=2 -e DRIVER_PATH=/chromedriver -e GIT_COMMIT=$(git rev-list -1 HEAD) mprr
    ```

### Execução sem Docker:

- Para executar o script é necessário rodar o seguinte comando, a partir do diretório mprr, adicionando às variáveis seus respectivos valores, a depender da consulta desejada. É válido lembrar que faz-se necessario ter o [Python 3.8+](https://www.python.org/downloads/) instalado, bem como o chromedriver compatível com a versão do seu Google Chrome. Ele pode ser baixado [aqui](https://chromedriver.chromium.org/downloads).
 
    ```sh
    $ YEAR=2018 MONTH=03 DRIVER_PATH=/chromedriver GIT_COMMIT=$(git rev-list -1 HEAD) python3 src/main.py
    ```
- Para que a execução do script possa ser corretamente executada é necessário que todos os requirements sejam devidamente instalados. Para isso, executar o [PIP](https://pip.pypa.io/en/stable/installing/) passando o arquivo requiments.txt, por meio do seguinte comando:
   
   ```sh
    $ pip install -r requirements.txt
   ```