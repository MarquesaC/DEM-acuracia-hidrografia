# DEM e sua acurácia através da hidrografia
Modelo Digital de Elevação _ extração da hidrografia
Este processo tem intenção de trabalhar com a acurácia de dados de satélite, através da extração da hidrografia, identificar o Modelo Digital de Elevação que tenha maior acurácia/ maior proximidade com a mofologia do terreno com a microbacia urbana Gregório do município de São Carlos- SP.

Observação importante: para cada passo de processamento é necessário salvar no arquivo da pasta para que posteriormente tenha a possibilidade de extrair os dados.

# A coleta de dados
Uma das relevâncias de trabalhar com imagens de satélite ou sensoriamento remoto é que o processo otimiza o tempo e custos para obter um estudo ou resultado de produtos.
Neste momento iremos trabalhar com Modelos Digitais de Elevação que são disponibilizados gratuitamente no software aberto QGIS versão 3.34 (LTR) disponibilizado em <https://www.qgis.org/download/>.
Os modelos digitais de elevação gratuitos e globais, na resolução espacial de 30 metros, foram obtidos pelo software livre QGIS 3.34, através do plugin Open Topography DEM Downloader.
1. Um dos primeiros passos é baixar os modelos NASA DEM; Copernicus; SRTM e ALOS DEM.
2. Ao selecionar os modelos dentro do plugin [Open Topography DEM Downloader] é interessante delimitar a extensão para a área de estudo pelo arquivo de vetor [Gregório] disponibilizado neste mesmo repositório.
3. No final dos processos os dados se encontrarão em formato raster, prontos para serem trabalhados. Os mesmos se encontram disponíveis no repositório.

# Limpeza dos dados e transformação dos dados
Para esta etapa os dados precisam passar por alguns tratamentos, se tratando de imagem de satélite como um MDE, é importante estar atendo aos valores que cada pixel carrega e elimnar possíveis dados falsos ou células [no data].
Para este processo de limpeza e extração dos dados, continuaremos com o software QGIS 3.34 utilizando a barra de ferramentas localizados na parte superior da janela do software e também é necessário instalar o complemento do GRASS para utilização em alguns processos específicos.
Dos itens 1 ao 7 se repetirão 4 vezes para cada uma das imagens raster obtidas, ao finalobteremos dados vetoriais para a análise.
Até este momento trataremos e extraimos os dados dos arquivos obtidos, mas para o fim comparativo precisamos combinar os dados para termos as informações relevantes para interpretação de dados, dos itens 8 ao 10 continuaremos com o software QGIS 3.34 utilizando a barra de ferramentas localizados na parte superior da janela do software. Desta forma estes também terão que ser repetidos para cada Modelo Digital de Elevação (MDE) combinando a hidrografia da carta topográfica.
1. Reprojetar coordenadas [ferramenta raster] - função de transformar o sistema de projeção de WFS 84 para SIRGAS 2000 UTM Zona 23S.
2. Preencher células no data [ferramenta rater] - função de preenchimento dos pixels vazios da imagem.
3. Neighbor [semi-automatic classification plugin] - função de suavização dos pixels para diminuir ruidos.
4. Direção de fluxo [r.watershed (plugin do GRASS)] - direcionamento de fluxo de água de acordo com o relevo.
5. Fluxo acumulado [r.terraflow (plugin do GRASS)] - Acumulação do fluxo de água de acordo com o valor do pixel e sua vizinhança.
6. Extrair drenagem [r.stream extract (plugin do GRASS)] - Extair pixel com maiores valores fluxo acumulado (este passo requer uma interpretação do usuário para definir o limiar ideal ou que achar adequado para a própria área de estudo, tendo como base a hidrografia da carta topográfica.
7. Sobreposição do arquivo original da hidrografia extraído através da carta topográfica que está disponibilizado em arquivo vetor [HIDRO_GREGORIO_CARTA] com cada hidrografia obtida pelo diferentes modelos de DEM.
8. União [Vetor - geoprocessamento] - Unir a camada vetorial da hidrografia da carta com a hidrografia gerada pelo MDE.
9. Poligonize [caixa de ferramentas - geometria do vetor] - Ao qual onde tiver as intersecções das linhas da hidrografia, irá criar um poligono que posteriormente será ultilizada o valor da área para determinar a distancia e a acurácia do relevo da bacia.
10. Com o arquivo gerado, iremos em camadas do painel e abrir a tabela de atributos de cada arquivo gerado do processamento anterior através do botão direito em cima da camada para calcular a área em metros quadrados para polígono de intersecção gerada entre as duas hidrografias (ir em calculadora de campo; nome da saida de campo; inserir: [AREA]; tipo de campo: número deciamal (real); na aba de expressão digitar: $area; clicar em [OK] para executar processo. IMPORTANTE REPETIR ESSE CÁLCULO PARA TODAS AS CAMADAS GERADAS.

# Análise dos dados
Para esta etapa iremos começar a analisar os dados obtidos através do geoprocessamento, assim, utilizaremos o EXCEL
Em um arquivo excel iremos compilar os dados para a análise, para acessar os dados do nosso passo do item 10, temos que ir em abrir aquivo do excel e na janela de pastas dos nossos processamentos no computador, escolher o tipo de arquivo [.dbf] para abrir. Assim que abrir selecionaremos a coluna área e copiaremos para o nosso excel para começar a análise das áreas. Sendo o DEM com menor área como a mais próxima da hidrografia real, portando podendo considerar como o DEM que tem a morfologia mais próxima do real da microbacia urbana.
