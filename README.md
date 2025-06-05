# 📄 Evidencia

En esta práctica, se busca desarrollar una pequeña interfaz de lenguaje natural controlado para emitir comandos a un robot virtual. Este robot es capaz de realizar acciones simples como moverse, girar y detenerse. Las instrucciones deben seguir una estructura clara, amable y definida, similar a cómo una persona se dirigía educadamente a un asistente robótico.  
El objetivo principal es contruir el analizador léxico (Lex) y un analizador sintáctico (YACC) capaces de procesar y validar un conjunto restringido de isntrucciones escritas en lenguaje natural simple.

---

## 🔍 Analizador léxico (LEX)

El analizador léxico tiene la tarea de leer una entrada que contiene instrucciones destinadas a un robot y desglosarla en unidades léxicas de importancia denominadas **tokens**. Estas unidades facilitarán al compilador la comprensión de los diferentes elementos de las frases, tales como:

- **Sustantivos**: indican entidades o elementos del entorno del robot (ej. `"Robot"`, `"blocks"`, `"degrees"`).  
- **Verbos**: describen las acciones que el robot puede ejecutar (ej. `"move"`, `"turn"`, `"stop"`).  
- **Palabras de cortesía**: ayudan a que las instrucciones sean más "humanas" y amables (ej. `"please"`, `"thank you"`).  
- **Números**: representan cantidades (`{1-10}`, `{90, 180, 270, 360}`).  
- **Conectores y preposiciones**: indican orden o dirección (ej. `"and"`, `"then"`, `"ahead"`, `"right"`).  

El analizador léxico debe tener la habilidad de identificar estas categorías, pasar por alto espacios o tabulaciones, y **informar sobre cualquier símbolo no identificado como error**.

---

### 📌 Definición de tokens

### ✅ Lista de ejemplos aceptados:

- Robot please move 3 blocks ahead, and then turn 90 degrees.  
- Please robot move 3 blocks, and then turn 360 degrees.  
- Robot please move 3 blocks ahead and then turn 90 degrees, then move 2 blocks  

### ❌ Ejemplos rechazados:

- Robot turn 80 degrees  
- Robot please move 8 blocks now.  
- Robot please turn 78 degrees  

---

## 🧠 Analizador sintáctico (YACC)

El analizador sintáctico necesita emplear los tokens suministrados por Lex para verificar si la secuencia de instrucciones satisface la gramática prevista. El objetivo es establecer una **gramática libre de contexto (CFG) no ambigua**, que facilite la identificación únicamente de aquellas frases que constituyan instrucciones válidas para el robot.

Las frases válidas deben satisfacer las siguientes propiedades:

- Iniciar siempre con la palabra `"Robot"`.  
- Usar formas educadas o directas pero correctas (como `"please move"`, `"turn"`, `"stop"`).  
- Incluir información suficiente sobre la acción: qué hacer, cuántos bloques avanzar, cuántos grados girar, etc. Cabe aclarar que deben de ser los números dentro del rango de lo que se pide.  

En cambio, el sistema debe tener la habilidad de **descartar frases ambiguas, incompletas o incorrectas**, como las que alteren el orden de las palabras, empleen términos no identificados o muestren una sintaxis confusa.

---

### 📐 Definición de CFG

```bnf
<STRUCTURE-SENTENCE> -> <REQUIREMENTS><SENTENCE>
<SENTENCE> -> <CMPLX-VERB>
<REQUIREMENTS> -> <SUBJECT> <COURTESY-WORD> | <COURTESY-WORD> <SUBJECT>
<CMPLX-VERB> -> <VERB-PHRASE> | <VERB-PHRASE> <CONNECTOR> <SENTENCE>
<VERB PHRASE> -> <STRUCTURE-PHRASE><PUNCTUATION> | <STRUCTURE-PHRASE><DIRECTION><PUNCTUATION>
<STRUCTURE-PHRASE> -> <VERB><NUMBER_BLOCK><INSTRUCTION> | <VERB><NUMBER_DIRECTION><INSTRUCTION>
<SUBJECT> -> Robot | robot
<COURTESY-WORD> -> Please | please
<CONNECTOR> -> and then | then | next | and finally
<PUNCTUATION> -> . | , | {empty string}
<DIRECTION> -> forward | ahead | backward
<VERB> -> move | turn
<NUMBER_BLOCK> -> 1 | 2 | 3 | 4 | 5 | 67 | 8 | 9
<NUMBER_DIRECTION> -> 90 | 180 | 270 | 360
<INSTRUCTION> -> degrees | blocks









