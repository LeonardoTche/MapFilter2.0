# MapFilter 2.0 Tutorial

## Configuração inicial

O sofware **MapFilter 2.0** processa dados númericos com separador decimal `.` (ponto). A configuração pode ser feita através do painel de controle:

Painel de controle > Relógio e Região > Alterar Formato de data, hora ou número > Configurações adicionais  

Em seguida altere os campos conforme abaixo:  

> Símbolo decimal: `.` (ponto)  
> Símbolo de agrupamento de dígitos: `,` (vírgula)  
> Separador de listas: `,` (vírgula)    


## Formato do arquivo de dados

O **MapFilter** processa um único conjunto de dados em um arquivo em formato de texto (`.txt` ou `.csv`) por vez. O arquivo de texto deve conter pelo menos *três atributos **numéricos_**: dois atributos contendo a **latitude** e **longitude** e o **atributo** que será submetido à filtragem.

### Importante

* A primeira linha do arquivo deve conter um cabeçalho (denominação) de atributos; 
* As coordenadas devem estar no datum WGS 84 ou equivalente fornecido em **coordenadas geográficas (graus decimais)**, que é uma forma comum para o armazenamento de coordenadas em registradores de dados agrícolas **ou** na forma **métrica (UTM)**; 
* As coordenadas precisam ter o cabeçalho nomeados com as iniciais **"Lat"** e **"Long"** ou **"X"** e **"Y"**.


## Filtragem dos dados

### Iniciar o software

Para iniciar o software **MapFilter 2.0** é só clicar no Menu Iniciar do Window. Em seguida ir na pasta **LAP USP** e clicar em **MapFilter**.<br/>

<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/telaIinicial.png?raw=True" width="700"/></a>          <br>  
  <em> Interface inicial </em>
</p>

### Selecionar arquivo

Neste tutorial iremos utilizar como exemplo dados de produtividade de milho.<br/>
 
Para abrir o conjunto de dados a ser filtrado clique em  [![image](https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/img2.png?raw="True")](#features) na tela inicial e selecione o arquivo [`corn_yield.txt`](/Exemplo/).<br/>

### Identificar o atributo a ser filtrado

Identifique o atributo a ser filtrado:<br/>
 
<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/img3.png?raw=True" width="300"/></a> 
</p> 
  

Os dados do atributo a ser filtrado são plotados no visor e a estatística descritiva é calculada:<br/>  
<br/>

<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/img4.png?raw=True" width="700"/></a>
     <br>
     <em> Visualização dos dados originais </em>
</p>
<br/>

### Filtragem global

O filtro global foi adicionado antes do filtro local para evitar a inflação de variações dos valores do atributo na análise local devido a valores muito baixos ou muito altos. No filtro global, a mediana dos valores do atributo em análise é usada para calcular os limites de corte superior (Eq. 1) e inferior (Eq. 2):
```
Limite Superior = mediana + mediana x v                                                                  Equação 1
Limite Inferior = mediana - mediana x v                                                                  Equação 2
```

O valor de ` v ` deve ser informado pelo usuário no campo `  Variation of limit (%)  `
  
<br/>

<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/filt_globalVar.png?raw=True" width="300"/></a> 
</p>

<br/>


No nosso exemplo iremos utilizar `v = 35`


Para realizar o filtragem global clique no ícone [![image](https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/img7.png?raw=true)](#features)  

<br>

Após a filtragem global o **MapFilter** plota e recalcula a estatistica descritiva dos dados remanecentes da filtragem. Neste exemplo a filtragem global eliminou todos os dados com valores de produtividade acima de 7.53 e abaixo de 3.63.<br/>  
<br/>
<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/filt_global.png?raw=True" width="700"/></a>
     <br>
     <em> Visualização dos dados após a filtragem global </em>
</p>


### Filtragem local

O **filtro local** foi dividido em duas etapas: filtro local anisotrópico e isotrópico. <br/> 
O _**filtro anisotrópico**_ detecta todos os pontos localizados em uma faixa de _**raio (R)**_ em torno de um ponto xi em uma _**única direção**_. O ponto xi é comparado com k vizinhos à frente e k vizinhos anteriores. O k é o número de vizinhos cuja distância euclidiana é menor ou igual ao R (linha azul na Figura). A mediana desses k vizinhos é calculada e a Eq. 1 e Eq. 2 são aplicados ao ponto xi. Se o valor do ponto xi for maior ou menor dos limites superior e inferior de corte, ele será considerado um erro local e será excluído do conjunto de dados.<br/>
O _**filtro isotrópico**_ detecta todos os k pontos vizinhos localizados em um _**R**_ em torno de um ponto xi em _**qualquer direção**_. Então, a mediana desses k vizinhos é calculada e as Eq. 1 e 2 são aplicadas ao ponto xi. O filtro exclui o ponto xi com um valor maior ou menor que os limites de corte superior e inferior.<br/>
<br/>
<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/esquema_pt.png?raw=True" width="700"/></a>
     <br>
     <em> Identificação dos pontos vizinhos na filtragem local </em>
</p>

<br/>

O valor do raio `R` deve ser informado pelo usuário no campo `Spatial Dependence (m)` e o valor de `v` deve ser informado pelo usuário no campo `Variation of limit (%)` <br/>
<br/>

<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/filt_localVar.png?raw=True" /></a>
     <br>
</p>
<br/>

No nosso exemplo iremos utilizar `R = 100` e `v = 5`


Para realizar o filtragem local clique no ícone [![image](https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/img7.png?raw=true)](#features)  

<br>

Após a filtragem local o **MapFilter** plota e recalcula a estatistica descritiva dos dados remanecentes da filtragem.<br/>  
<br/>

<p align="center">
     <a href="#"><img src="https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/filt_local.png?raw=True" width="700"/></a>
     <br>
     <em> Visualização dos dados após a filtragem local </em>
</p>
<br/>

### Salvar os dados

Os dados que não foram excluídos pelo filtro podem ser salvos em um arquivo tipo texto (`.txt` ou `.csv`).<br/> 

Para salvar os dados clique no ícone [![image](https://github.com/LeonardoTche/MapFilter2.0/blob/master/Tutorial/Img/salvar.png?raw=true)](#features) 
