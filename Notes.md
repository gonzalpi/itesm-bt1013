<style>
    p {text-align: justify;}
    h2 {text-align: center;}
    h4 {text-align: right;}
    table {margin: auto;}
    /*  h1 : unit name
        h2 : main topic
        h3 : subtopics
        h4 : date       */
</style>



# Computational Biology
BT1013 Section 829

#### March 23

## Data types and data structures

> Source: [https://swcarpentry.github.io/r-novice-inflammation/13-supp-data-structures/](https://swcarpentry.github.io/r-novice-inflammation/13-supp-data-structures/)

Data types:
- character
- numeric
- integer
- logical
- complex

Data structures:
- vector
    - atomic: single type data
    - list: multiple types
- matrix
- data frame
- factors

Object attributes:
- ```class()``` : kind of object
- ```typeof()``` : object's data type
- ```length()``` : vector/list length
- ```nchar()``` : string size
- ```dim()``` : array dimensions
- ```attributes()``` : metadata
- ```names()``` : list elements names

Missing data: ```NA```
- ```is.na()``` : returns logical vector with ```TRUE``` for each missing value
- ```anyNA()``` : ```TRUE``` if there's any ```NA```

Infinity: ```Inf``` (can be + or -)

Not a Number: ```NaN``` (undefined)

### Vector
- ```vector()``` : empty logical vector
- ```logical(1)```: same as above
- ```vector("character", length=sz)```: mode "character" vector of length ```sz```
- ```character(sz)``` : same as above
- ```numeric(sz)``` : mode "numeric" vector
- ```c()``` : combine function (implicitly coerces to single type)
- ```c(1L, 2L, 3L)``` : mode "integer" vector containing 1, 2, 3 as ```int```
- ```c(TRUE, FALSE)``` : mode "logical" vector
- sequence of numbers:
    - ```1:10``` : vector from 1 to 10 in increments of 1
    - ```seq(10)``` : same as above
    - ```seq(from=1, to=10, by=1)``` : same as above
- ```as.<class_name>()``` : explicitly coerces vectors to class

### Matrix
- filled column-wise
- ```byrow = TRUE``` : forces row-wise fill
- ```matrix(nrow=x, ncol=y)``` : x-by-y matrix
- ```matrix(1:6, nrow=2, ncol=3)``` : 2-by-3 matrix containing ```[1 3 5 ; 2 4 6]```
- alternate method 1:

        m <- 1:6
        dim(m) <- c(2,3)

- alternate method 2 (column bind):

        c1 <- c(1, 2)
        c2 <- c(3, 4)
        c3 <- c(5, 6)
        m <- cbind(c1, c2, c3)

- alternate method 3 (row bind):

        r1 <- c(1, 3, 5)
        r2 <- c(2, 4, 6)
        m <- rbind(r1, r2)

- ```m[x, y]``` : access element in x-th row and y-th column

### List
- ```list(1, "a", TRUE, 3+4i)``` : list containing four elements of different data types
- ```as.list()``` : coerces other objects
- ```vector("list", length=sz)``` : empty list of length ```sz```
- ```list(alpha="Bravo", charlie=1:10)``` : list containing to named elements
- ```li[[x]]``` : access x-th element in list
- ```li$alpha``` : access element named alpha in list

### Data frame
- rectangular list (every element has the same length)
- can be accessed like lists
- attributes:
    - ```rownames()``` : to annotate ```subject_id``` or ```sample_id```
- usually created by ```read.csv()``` and ```read.table()```
- ```data.matrix()``` : converts data frame into table
- ```data.frame()``` : new data frame
- ```data.frame(id=letters[1:5], x=6:10)``` : data frame with letters a-e and numbers 6-10

Data frame functions:
- ```head()``` : shows first 6 rows
- ```tail()``` : shows last 6 rows
- ```str()``` : structure of data frame (name, type, preview of data in each column)
- ```sapply(dataframe, class)``` : shows class of each column

### Summary

| Dimensions    | Homogenous    | Heterogenous  |
| ---           | ---           | ---           |
| 1D            | atomic vector | list          |
| 2D            | matrix        | data frame    |

## Functions

    name <- function(arguments) {operation}
    add <- function(x, y) {x + y}

#### Apr 6

## Bioelementos

### Macromol??culas

- Mon??mero: unidad b??sica (e.g. mol??cula de glucosa)
- Doble enlace facilita reacciones
- Elementos m??s abundantes: C, H, O, N, P, S
    - C: base, andamiaje (en teor??a tambi??n puede servir Si)
    - P: parte de fostol??pidos en membranas celulares, uni??n de mol??culas
    - S: formacion de amino??cidos (ciste??na y metionina)
- Tipos:
    - Carbohidratos
        - Fuente primaria de energ??a
        - Tienen C, H, O, en proporci??n 1:2:1
    - L??pidos
        - Insolubles en agua
        - S??lidos a temperatura ambiente (insaturados son l??quidos)
        - Delimitar, dar estructura al cuerpo
        - Almacenamiento m??s r??pido para energ??a
    - Prote??nas
        - Pol??meros de aminoacidos
        - 50% de peso seco de c??lula es prote??na
        - Estructura:
            1. Primaria: secuencia de cadena de amino??cidos
            2. Secundaria: amino??cidos en secuencia interact??an por enlaces de H
            3. Terciaria: ciertas atracciones entre h??lices alfa y hojas plegadas
            4. Cuaternaria: prote??na que consiste de m??s de una cadena
        - Orden de amino??cidos determina estructura tridimensional
        - Estructura tridimensional determina funci??n
        - Tipos:
            - Catalizadores (enzimas)
            - Transporte (hemoglobina)
            - Estructurales (col??geno)
            - Homeostasis (alb??mina)
            - Defensa (anticuerpos)
            - Hormonas (insulina, hormona de crecimiento)
            - Locomoci??n (actina, miosina)
    - ??cidos nucleicos: compuestos de biomol??culas con pero molecular de 25k a 3M, cadenas de nucle??tidos
        - Tipos:
            - ADN
            - ARN
        - Nucle??tidos (mon??meros):
            - Az??car (pentosa): desoxiribosa (tiene un ox??geno menos, es m??s estable) o ribosa
            - Unidos por grupo fosfato (-P)
            - Base nitrogenada
                - P??rica (derivada de purina): guanina G, adenina A.
                - Pirim??dica (derivada de pirimida): citosina C, timina T, uracilo U.

        ![Image](Notes/acidosNucleicos.png)

### ADN

Pol??mero de nucle??tidos. Puede duplicarse antes de la divisi??n celular. Dentro de cromosomas est??n los genes formados por ADN que contiene info. para hacer prote??nas.
- Las cadenas son antiparalelas (una empieza de 5' a 3' y la otra de 3' a 5')
- Interacciones:
    - CG (3 enlaces de H)
    - AT (2 enlaces de H)
- Estructura:
    - Primaria: secuencia de nucle??tidos (orden y orientaci??n)
        - Los carbonos se cuentan a partir de la base nitrogenada
        - Cada cadena tiene extremo 5' porque tiene un grupo fosfato libre unido al carbono 5' del nucle??tido. Tiene un extremo 3' porque tiene un OH- en la posici??n 3' del nucle??tido
        ![Image](Notes/nucleotido.jpeg)
        - La otra cadena va de 3' a 5'; 5' representa el extremo terminal del fosfato y 3' el estremo final del ??tomo de carbono del az??car (se une a otra mol??cula).
        ![Image](Notes/desoxirribosa.jpeg)
        - Sentido de lectura: 5' a 3'
    - Secundaria: doble h??lice antiparalela con bases nitrogenadas unidas por puentes de hidr??geno otorgando estabilidad
    - Terciaria: empaquetamiento del ADN, cromatina (forma compacta)
        - Niveles:
            - Nucleosoma: circulos de prote??na
            - Collar de perlas: donde nucleosomas aparecen enrollados
            - Fibras cromat??nicas: donde el collar se enrolla en s?? formando un solenoide
            - Bucles radiales: durante interfase de ciclo celular, compactaci??n hasta formar cromosomas

### ARN

Cadena que puede enrollarse en s?? misma hasta formar h??lice de una sola cadena. Copia ADN para producir prote??nas, une amino??cidos en orden correcto, forma ribosomas.
- Estructura primaria: igual que ADN pero de menor tama??o
- Tipos:
    - Mensajero (ARNm): copia info. gen??tida de ADN
    - De transferencia (ARNt): une los 20 amino??cidos en la s??ntesis de prote??nas (los transporta del citoplasma al ribosoma)
    - Ribosomal (ARNr): forma ribosomas con prote??nas
- Interacciones:
    - CG (3 enlaces de H)
    - AU

### Dogma central de la biolog??a molecular

    Replicaci??n:    ADN -> ADN
    Transcripci??n:  ADN -> ARN
    Traducci??n:     ARN -> Prote??na

ARNm copia informaci??n de ADN, la saca del n??cleo y la lleva a los ribosomas. ARNt transporta informaci??n para sintetizar prote??nas.

Gen: regi??n de ADN que codifica para una funci??n en espec??fico (e.g. color de ojos)

ARNm, traducci??n: codones de 3 nucle??tidos (4 posibles estados c/u) -> 64 combinaciones =  64 prote??nas
- Estructura:
    - Cap
    - 5' UTR (untranslated region)
    - CDS (coding sequence from start to stop)
    - 3' UTR (untranslated region)
    - Poly-A tail
- Pre-ARNm
    - Exon: regi??n que da informaci??n (que se pasa a CDS en ARNm)
    - Intron: regi??n que NO da informaci??n (no se pasa a CDS)

ARN est?? basado en cadena complementaria de cadena ADN

Marco de lectura:
- AUG/ATG es el inicio (en bases de datos nunca hay U) para ARN
- TAC es el inicio para ADN (complementario de ATG)

#### April 13

## Databases

Genes (NCBI):
- Standardized names provided by HGNC (HUGO Gene Nomenclature Committee)
- RefSeq status: REVIEWED means it exists and its functions have been proven
- Gene location: 11p15.5
    - 11th largest chromosome
    - p bras pour petit (ou q pour le grand)
    - 15th band across arm
    - 5th sub band
- Exon count: n??mero de regiones que s?? se codifican
- FASTA: sequence in nucleotides
- GenBank: sequence in aminoacids

#### April 16

## Virus

Par??sitos moleculares

![Image](Notes/genomasVirales.png)

Prebi??tico: alimento para probi??tico (e.g. yogurt, kombucha)

Probi??tico: alimentos con microorganismos para fortalecer bacterias ben??ficas del cuerpo (e.g. Yakult)

Antibi??tico: mata a TODAS las bacterias

Superbug: bacteria que ha sobrevivido a todos los antibi??ticos

### Virome

![Image](Notes/virome.png)

Colecci??n de virus en el cuerpo humano
- Virus no ben??ficos: VIH, papiloma humano, etc.
- Virus que se quedan en los test??culos/ovarios: se heredan

Retrovirus: RNA a DNA, se introduce a genoma

Para introducir DNA: disparar, electrocutar o choque t??rmico

## SARS-CoV 2

- Familia: coronaviridae
- G??nero: coronavirus
- Genoma: 29 903 letras
- Proteina Spike: se conecta con el host, parte m??s importante
    - Genoma de CoV humano es distinto en la parte del Spike del murci??lago y pangol??n, y por eso no les afecta como a nosotros

### Coronavirus humanos
M??s comunes:
- 229E
- NL63
- OC43
- HKU1

Otros m??s graves:
- MERS-CoV
- SARS-CoV
- SARS-CoV 2 *(covid-19)*

#### April 20

## Plotting in R

    par(mar = c(1,1,1,1)) // to set margins
    par(mfrow = c(2,2)) // plot grid dimensions
    
    str(dataframe) // string summary
    hist(dataframe$variable) // histogram
    with(dataframe, plot(var1, var2)) // another way of plotting
    
    var <- read.csv("file.csv", header=TRUE; stringAsFactors=FALSE)
    head(diseases) // displays first 6 entries
    tail(diseases) // displays last 6 entries
    
    table(dataframe$variable) // counts occurrence of each entry (histogram with discrete/qualitative data types)
    
### ```ggplot```

Datos + Est??tica + Capas + Facetas()

        library(dplyr)
        barplot(table(dataframe$variable))
        dataframe$variable %>% table %>% barplot
        
        library(stringr) // string manipulation

## Alineaci??n

### Gen??mica comparada

Estudio de relaci??n entre estructura y funci??n de genoma
- A partir de similitudes y diferencias de prote??nas, ARN y regiones reguladoras
- Selecci??n:
    - Estabilizadora: elementos responsables de similitudes que se conservan en el tiempo
    - Positiva: elementos responsables de diferencias entre especies que diviergen
    - Neutral: elementos que no son importantes para el ??xito evolutivo

Relaciones entre genes
- Analog??a: misma funci??n, diferente origen
- Homolog??a: genes similares de ancestro com??n, misma o diferente funci??n
- Genes ort??logos: mismos genes en distintas especies
- Genes par??logos: derivados de una duplicaci??n en un organismo, misma o diferente funci??n
- Conversi??n g??nica: sustituci??n de segmento de ADN de un gen con segmento hom??logo de su par??logo

??Para qu?? sirve la alineaci??n?
- Descubir genes hom??logos
- Encontrar patrones de conservaci??n
- Construir taxonom??as (estudios filogen??ticos)
- Estudios poblacionales (SNIPs)
- Dise??o de cebadores (primers)
    - identificar regiones espec??ficas mediante amplificaci??n (e.g. prueba PCR)
- Identificar prote??nas similares: predecir funciones y estructura
- Identificar genes y funci??n
- Identificar secuencias repetidas en tandem
    - ??rea forense, pruebas de paternidad
- Identificar regiones funcionales: origen de replicaci??n, sitio de uni??n al ribosoma, etc.
- Identificar mutaciones (enfermedadres)
    - tomar decisiones sobre alimentaci??n, cuidados corporales y operaciones quir??rjicas
- Localizar secciones de ADN solapadas: ensamblaje
    - secuenciaci??n, ensamblar secuencias parciales

Comparaci??n de secuencias
1. Se colocan 2 de manera paralela
2. Se genera una funci??n de puntuaci??n a maximizar (match, mismatch, gap penalty)

Alineamiento:
- Global: tomar cadenas de longitud similar y comparar (e.g. comparar SARS-CoV y SARS-CoV-2)
- Local: tomar partes y comprarar (e.g. comparar SARS-CoV-2 e influenza)

M??todos:
- A mano
- Bioinform??tica:
    - An??lisis de Dot Plot
    - Algor??tmos de Programaci??n Din??mica
    - Heur??sticas (BLAST): identifica hom??logos y regiones de semejanza (alineamiento local)
        - BLAST NCBI

#### April 27

## ??rboles filogen??ticos


Libraries:

    library(ape)
    library(phangorn)
    library(phytools)
    library(geiger)
    library(ggmsa)
    library(Biostrings)
    library(seqinr)
    library(adegenet)
    library(ape)
    library(ggtree)
    library(DECIPHER)
    library(viridis)
    library(ggplot2)

Los elementos de acomodan de abajo hacia arriba.

    vert.tree("(cow,(pig,tree));")
    
    #    .-- tree
    # .--|
    # |  '-- pig
    # |
    # '----- cow

Endograma: muestra relaciones

??rbol filogen??tico (tb. an??lisis jer??rquico global): muestra grados de relaci??n (distancias proporcionales)