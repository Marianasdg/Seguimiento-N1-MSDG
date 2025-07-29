# Seguimiento-N1-MSDG
Desarrollo del seguimiento #1 de la asignatura Bioinformatica. Por: Mariana Salazar Diaz Granados

## ¿Qué campos tiene un archivo GFF3 y qué información contienen?

Un archivo GFF3 es un formato de texto delimitado por tabulaciones que se utiliza para describir características del genoma, como la ubicación de genes, exones, CDS, entre otros. Este formato organiza la información en líneas que representan anotaciones específicas, y cada una de ellas está compuesta por **9 columnas obligatorias** que facilitan la descripción detallada de los elementos genómicos. A continuación, explico cada columna con ejemplos prácticos:
---

### **1. seqid**
Indica en qué secuencia está la anotación, por ejemplo, el cromosoma o el contig.
**Ejemplos:**
1
10
scaffold_12

---

### **2. source**
Es la herramienta o base de datos que realizó la anotación.
**Ejemplos:**
ensembl
maker

---

### **3. type**
El tipo de elemento anotado. Puede ser un gen, un mRNA, un exón, etc.
**Ejemplos:**
gene
mRNA
exon
CDS
five_prime_UTR

---

### **4. start y 5. end**
Son las coordenadas donde empieza y termina la anotación.
**Ejemplo:**
24225   56222
Esto significa que el feature va desde la posición 24,225 hasta la 56,222.

---

### **6. score**
La calidad de la anotación. Si no hay valor, se pone un punto (.).
**Ejemplos:**
.
0.98

---

### **7. strand**
Indica en qué hebra se encuentra la anotación:
+ → hebra directa
- → hebra complementaria
. → no aplica

Ejemplos:

+ → El gen ABC1 se encuentra en la hebra directa.
- → El gen XYZ2 está ubicado en la hebra complementaria.
. → El elemento regulador no se asocia a una hebra específica.



---

### **8. phase**
Solo aplica para CDS. Indica en qué marco empieza la traducción: 0, 1 o 2. Si no aplica, se pone un punto.
**Ejemplos:**
0
.

---

### **9. attributes**
Información extra en pares clave=valor, separados por ;.
**Ejemplos:**
ID=gene:ENSPERP00000012345;Name=emilin1b;biotype=protein_coding
ID=transcript:ENSPERT00000023456;Parent=gene:ENSPERP00000012345;biotype=protein_coding

---

### **Ejemplo completo de una línea GFF3**
1   ensembl   gene   24225   56222   .   +   .   ID=gene:ENSPERP00000012345;Name=emilin1b;biotype=protein_coding

---

## **Descripción del Organismo**
El organismo asignado es **Amphiprion percula**, mejor conocido como pez payaso naranja. Dicho organismo vive en arrecifes de coral del Océano Índico y Pacífico y es famoso por su relación simbiótica con las anémonas marinas. Este organismo es importante para estudios genómicos porque tiene genes relacionados con adaptación marina y simbiosis. En el archivo GFF que descargamos desde Ensembl, encontramos anotaciones de genes, regiones codificantes, exones, ARN no codificantes y más (Graham, 2016).

*Webgrafía*: Graham, K. S. (2016). Status Review Report: Orange Clownfish (Amphiprion percula). https://doi.org/10.13140/RG.2.1.3934.3843

---

## **Preguntas y Respuestas**

### **1. ¿Cuántos *features* contiene el archivo?**
Para contar todas las anotaciones que no son comentarios, usamos el comando:
grep -v "^#" Amphiprion_percula.Nemo_v1.114.gff3 | wc -l
En mi caso, el archivo tiene **836302** features.

---

### **2. ¿Cuántas regiones de la secuencia (cromosomas) contiene el archivo?**
Las regiones están en las líneas que empiezan con ##sequence-region:
grep "^##sequence-region" Amphiprion_percula.Nemo_v1.114.gff3 | wc -l
Resultado: **365** regiones.

---

### **3. ¿Cuántos genes están listados en el organismo?**
Para esto, busco solo las líneas donde la tercera columna es gene:
grep -P "\tgene\t" Amphiprion_percula.Nemo_v1.114.gff3 | wc -l
Resultado: **23926** genes.

---

### **4. ¿Cuál es el top 10 de tipos de features más anotados?**
Para contar la frecuencia de cada tipo y mostrar los 10 más comunes:
grep -v "^#" Amphiprion_percula.Nemo_v1.114.gff3 | cut -f3 | sort | uniq -c | sort -nr | head -10

Resultado en mi ejecución:

- 356757 exon
- 348151 CDS
- 34931 mRNA
- 29434 biological_region
- 23926 gene
- 23647 five_prime_UTR
- 17209 three_prime_UTR
- 875 ncRNA_gene
- 407 rRNA
- 365 region
---
