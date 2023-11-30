La información de contenida dentro de una célula es el genoma.
No todo el genoma se encuentra en cromosomas, en celulas eucariotas, parte de este se encuentra en los plásmidos. 
Un gen es localizable si este se encuentra en un sitio determinado del genoma y puede ser manipulado.

Las partes principales de un gen son:
- Promotor: 
	- region que regula la expression del gen al permitir/prevenir el ensamblaje del ribosoma. 
	- Los promotores constitutivos permiten la continua transcripcion del gen. 
	- Los promotores inducibles son aquellos que pueden ser activados/desactivados, por ejemplo por factores de transcripcion.
- Ribosome Binding Site
- Secuencia codificante (CDS)
- Terminador: Separa a la ARN polimerasa
Transcripcion: DNA-> mRNA
Traduccion: mRNA -> proteina

Fases de la transcripcion:
1. Iniciación: RNA polimerasa se ancla al promotor y comienza transcripcion.
2. Elongación: RNA polimerasa lee los nucleotidos hasta llegar al terminador
3. Terminación: RNA polimerasa se despega en el terminador para empezar el proceso de nuevo.

La mRNA va a contener el RBS y el CDS, posiblemente de varias proteinas. 

La traduccion se lleva a cabo por los ribosomas

Fases de la traduccion:
1. Iniciación: Anclamiento del ribosoma
2. Elongacion: Empieza con la lectura del codon de inicio AUG, y siguiendo.
3. Terminación: El ribosoma detecta alguno de los codones de terminacion: UAA, UAG, o UGA

Los enlaces peptidicos son un tipo de enlace covalente entre dos aminoacidos alfa en C1-N2 a lo largo de la cadena de peptidos o proteina

Dentro de la categoria de proteinas funcionales se encuentran las enzimas.

Partes de una enzima:
- Sitio de reconocimiento (Recognition Site)
- Sitio de interaccion (Binding Site)
- Sitio catalitico (Active Site)

Flujo de trabajo de la ingenieria genética:
- Obtener la secuencia
- Clonarla
- Introducir a chasis u huesped
- Crecerlo en las condiciones correctas

La eleccion de promotores, RBS y terminadores debe ser basada en bibliografía previa para el chasis de elección

Para la CDS se puede buscar secuencias basadas en los organismos productores originales

Para introducir la secuencia deseada en el chasis se necesita un vehiculo, al cual llamamos vector. Estos por lo general son plasmidos bacterianos sinteticos.

Elementos de los vectores:
1. Sitio de origen de replicacion
2. Marcador de selección: ayuda a identificar a los organismos que contengan el vector, eg. resistencia a antibioticos. 
3. Sitio de clonación multiple: contiene multiples sitios de restriccion los cuales permiten la insercion del fragmento de ADN
Los microorganismos competentes sona quellos que pueden captar ADN exógeno.
El metodo de introduccion del vector depende principalmente del tipo de chasis a usar.

Principios de la biologia sintética:
- Abstracción: ADN -> dispositivos -> sistemas
- Modularidad: same as cs
- Estandarización: distintos fragmentos pueden unirse en partes funcionales
- Modelado: modelado matematico y computacional antes de lab

Las partes biologicas (biobricks) son las secuencias que codifican una funcion especifica. 

El metodo tradicional de Biobricks consiste en un prefijo y un sufijo en cada secuencia.
Prefijo: GAATTCGCGGCCGCTTCTAGAG
Contiene los sitios de restricción para las enzimas EcoR1 y Xba1

Sufijo: TACTAGTACGGGCCGCTGCAG
Contiene los sitios de restricción para Spe1 y Pst1

Enzimas de restricción: reconocen secuencias especificas de ADN (sitios de restricción) donde se unen para realizar un corte especifico, ya sea blunt-ends o sticky-ends. Estos ultimos permiten que dos fragementos de ADN previamente cortados puedan ser ligados por la complementariedad de los extremos.

Sitio de restricción Xba1: T^CTAG_A
Sitio de restricción Spe1: A^CTAG_T

Estos dos generan sticky-ends compatibles, generando una secuencia "scar" que ninguna de las dos enzimas puede reconocer: TCTAGA

Ejemplo:

Queremos utilizar los siguientes Biobricks:
Biobrick 1 (Promoter + RBS):
	--- E X |||||||| S P --- 
Biobrick 2 (CDS + Terminator):
	--- E X |||||||| S P ---
	
Podemos cortarlos para tener:
	--- E X |||||||| S P --- $\rightarrow$(E+S)$\rightarrow$ E X |||||||| S
Y:
	--- E X |||||||| S P --- $\rightarrow$(X+P)$\rightarrow$ X |||||||| X P
	
Y utilizamos el vector:
	---E X ~~~ S P---
Con el corte: 
	---E X ~~~ S P--- $\rightarrow$(E+P)$\rightarrow$ ---E ~~~ P---

Ahora podemos utilizar ligasa para obtener:
	---E X |||||||| |||||||| S P ---
Nótese que se mantuvieron los prefijos y sufijos. 

Los terminadores por lo general forman un stemloop y son ricas en GCs.
Las secuencias repetitivas son dificiles de sintetizar.
No puede contener otros sitios de restriccion que no sean el prefijo/sufijo

Operon: sistemas de regulacion genetica en bacterias y en los que los genes que codifican proteinas funcionalmente relacionadas se agrupan dentro del genoma
(Cluster of DNA under the same promoter)

###### Tags
#Genetics #MolecularBiology #Bioinformatics #SyntheticBiology #Microbiology #Biotechnology