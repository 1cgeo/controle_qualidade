# Conjunto de Ferramentas para Controle de Qualidade
Conjunto de ferramentas desenvolvidas no software [FME Workbench 2018](https://www.safe.com/) para executar o controle de qualidade de dados geoespaciais

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

### Medida existência de erro de conectividade altimétrica
* (6.3.1) Feições da classe *Trecho_Drenagem* devem possuir conectividade altimétrica (snap 3D)

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