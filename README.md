# Conjunto de Ferramentas para Controle de Qualidade
Conjunto de ferramentas desenvolvidas no software [FME Workbench 2018](https://www.safe.com/) para executar o controle de qualidade de dados geoespaciais.

Tais ferramentas tem a finalidade atender as obrigações do 1º Centro de Geoinformação (1ºCGEO) previstas na alínea "b", do item IV da CLÁUSULA TERCEIRA do Termo de Convênio Nº384/2017 FPE/RS e 17-113-00/EME, firmado entre o Exército Brasileiro e o Estado do Rio Grande do Sul, no que diz respeito a avaliação da qualidade dos produtos geoespaciais elaborados dentro do escopo do Contrato de Serviços de Consultoria PROREDES BIRD/RS (Nº 05/2017), firmado entre a Secretaria de Planejamento, Governança e Gestão (SPGG/RS) e a empresa Hiparc Geotecnologia, Projetos e Aerolevantamentos Ltda.

A seguinte documentação foi utilizada como referência para realização do controle de qualidade:
* ET-CQDG – Norma da Especificação Técnica para Controle de Qualidade de Dados Geoespaciais, 1ª edição (2016)
* ET-PCDG – Norma da Especificação Técnica para Produtos de Conjuntos de Dados Geoespaciais, 2ª edição (2016)
* ET-EDGV – Especificação Técnica para a Estruturação de Dados Geoespaciais Vetoriais, versão 2.1.3 (2010)
* ET-ADGV – Especificação Técnica para a Aquisição de Dados Geoespaciais Vetoriais,versão 2.1.3 (2011)
* Termo de Convênio Nº 384/2017 FPE/RS e 17-113-00/EME
* ESRI Shapefile Technical Description (1998)
* OpenGIS Implementation Specification for Geographic information – Simple Feature Access – Part 1: Common Architecture (2010)

---

## Verificação da qualidade de vetores de hidrografia
Esta ferramenta visa executar um controle de qualidade automatizado das seguintes classes previstas na ET-EDGV:
* *Trecho_Drenagem*
* *Massa_Dagua*
* *Trecho_Massa_Dagua*
* *Barragem*
* *Ilha*
* *Queda_Dagua*

Para realizar o controle de qualidade também é utilizada a classe *Curva_Nivel*.

A ferramenta está disponível em [Verificação da Qualidade da Hidrografia](https://github.com/1cgeo/controle_qualidade/blob/master/verificacao_qualidade_hidrografia.fmw).

### Medida existência de itens que violam regras de aquisição
* (4.3.1) Largura mínima de uma feição de *Trecho_Massa_Dagua* é de 20 metros na escala 1:25.000
* (4.3.2) Feições das classes *Massa_Dagua* e *Trecho_Massa_Dagua* com tipo *Represa/Açude* devem intersectar uma feição da classe *Barragem*
* (4.3.3) Feições da classe *Massa_Dagua* não devem conter feições da classe *Trecho_Drenagem*
* (4.3.4) Feições da classe *Trecho_Massa_Dagua* devem conter feições da classe *Trecho_Drenagem*
* (4.3.5) Feições das classes *Massa_Dagua* e *Trecho_Massa_Dagua* que intersectam uma feições da classe *Barragem* devem possuir tipo *Represa/Açude*
* (4.3.6) Feições da classe *Barragem* devem intersectar elementos das classes *Massa_Dagua* e *Trecho_Massa_Dagua*

### Medida existência de desnível incompatível
* (4.4.1) Feições da classe *Trecho_Drenagem* que possuirem um desnível (diferença entre coordenadas Z sucessivas) superioes a 10 metros devem conter feições da classe *Queda_Dagua*

### Medida existência de itens que violam regras da lei do modelado
* (4.5.1) Feições da classe *Trecho_Drenagem* não devem intersectar mais de uma vez um único elemento da classe *Curva_Nivel*
* (4.5.2) Feições da classe *Trecho_Drenagem* devem possuir sua coordenada Z de forma decrescente
* (4.5.3) Feições da classe *Massa_Dagua* devem apresentar coordenada Z constante

### Medida existência de geometrias inválidas
* (6.1.1) Feições devem ser válidas de acordo com o estipulado em [OGC Simple Features](http://www.opengeospatial.org/standards/sfa)

### Medida existência de sobreposição inválida
* (6.2.1) Feições das classe *Massa_Dagua* e *Trecho_Massa_Dagua* não devem possuir sobreposição
* (6.2.2) Feições da classe *Ilha* não devem sobrepor feições das classes *Massa_Dagua* e *Trecho_Massa_Dagua
* (6.2.3) Feições das classes *Trecho de Drenagem* e *Barragem* não devem se sobrepor.

### Medida existência de erro de conectividade altimétrica
* (6.3.1) Feições da classe *Trecho_Drenagem* devem possuir conectividade altimétrica (*snap* 3D)

### Medida existência de atributos quantitativos incorretos
* (7.2.1) O valor do atributo *altura* para a classe *Queda_Dagua* deve ser coerente com o desnível da feições da classe *Trecho_Drenagem* correpondente

### Medida presença de feições duplicadas
* (8.1.1) Não devem existir feições duplicadas

---

## Verificação da qualidade de vetores de altimetria

Esta ferramenta visa executar um controle de qualidade automatizado das seguintes classes previstas na ET-EDGV:
* *Curva_Nivel*
* *Ponto_Cotado*

Para realizar o controle de qualidade também são utilizadas as classes *Massa_Dagua* e *Trecho_Massa_Dagua*.

A ferramenta está disponível em [Verificação da Qualidade da Altimetria](https://github.com/1cgeo/controle_qualidade/blob/master/verificacao_qualidade_altimetria.fmw).

### Medida existência de itens que violam regras de aquisição
* (4.3.1) Feições da classe *Curva_Nivel* não podem ter sobreposição com feições da classe *Massa_Dagua*
* (4.3.2) Feições da classe *Curva_Nivel* devem somente cruzar feições da classe *Trecho_Massa_Dagua*
* (4.3.3) Feições da classe *Ponto_Cotado* não podem estar contidas em feições das classes *Massa_Dagua* e *Trecho_Massa_Dagua*
* (4.3.4) A coordenada Z de feições da classe *Ponto_Cotado* devem estar coerentes em relação a feição da classe *Curva_Nivel* a qual está contida
* (4.3.5) Feições da classe *Curva_Nivel* não devem formar um delgado com distância inferior a 10 metros
* (4.3.6) Não devem existir variações de coordenada Z em feições da classe *Curva_Nivel*

### Medida existência de geometrias inválidas
* (6.1.1) Feições devem ser válidas de acordo com o estipulado em [OGC Simple Features](http://www.opengeospatial.org/standards/sfa)

### Medida existência de sobreposição inválida
* (6.2.1) Feições das classe *Curva_Nivel* não devem possuir sobreposição
* (6.2.2) Feições das classe *Ponto_Cotado* não devem sobrepor feições da classe *Curva_Nivel*

### Medida presença de feições duplicadas
* (8.1.1) Não devem existir feições duplicadas

### Medida existência de itens ausentes (omissão)
* (8.4.1) Todos os cocurutos (feições da classe *Curva_Nivel* fechadas que não contenham outras) devem possuir pelo menos uma feição da classe *Ponto_Cotado*

## Verificação dos vizinhos do MDE
Esta ferramenta visa verificar a diferença dos valores dos pixels na área de sobreposição entre MDEs (MDT ou MDT).

A ferramenta está disponível em [Verificação dos vizinhos do MDE](https://github.com/1cgeo/controle_qualidade/blob/master/verificacao_vizinhos_mde.fmw).

## Verificação da aderência do MDT com hidrografia
Esta ferramenta visa verificar a diferença média de coordenadas do trecho de drenagem e MDT.

A ferramenta está disponível em [Verificação da aderência com hidrografia](https://github.com/1cgeo/controle_qualidade/blob/master/verificacao_aderencia_hidrografia_mdt.fmw).

## Geração de raster de diferença entre MDS e MDT
Esta ferramenta visa gerar o raster de diferença entre MDS e MDT.

A ferramenta está disponível em [Geração de raster de diferença entre MDS e MDT](https://github.com/1cgeo/controle_qualidade/blob/master/gera_diferenca_MDS_MDT.fmw).