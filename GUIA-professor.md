# Quiz Arena — Guia ràpida del professor

Joc de preguntes en directe tipus Kahoot per a l'aula. Tu projectes la pantalla amb
el PIN i les preguntes; cada alumne entra des del seu dispositiu, respon
contrarellotge i guanya punts per encert i rapidesa.

És **una sola pàgina web** (`index.html`). No hi ha servidor propi: les dades
(quizzes, llistes de classe, partides i historial) viuen a **Firebase Realtime
Database**, així que les veus des de qualsevol ordinador que obri la mateixa pàgina.

---

## 1. Com hi entres

| Qui | Adreça |
|-|-|
| **Alumnes** | l'adreça de la pàgina, tal qual |
| **Professor** | la mateixa adreça **acabada en `#host`** |

Exemple: si la pàgina és `https://elmeuusuari.github.io/quiz/`, tu entres a
`https://elmeuusuari.github.io/quiz/#host`. També funciona obrint el fitxer
`index.html` local al navegador i afegint `#host` al final de l'adreça.

> L'adreça exacta que han d'escriure els alumnes te la mostra la mateixa app a la
> pantalla del PIN ("Entra a … i posa el PIN").

Ara mateix **no hi ha contrasenya de professor** (`HOST_PIN = ""` dins del codi).
Si en vols una, edita aquesta línia a `index.html`; llavors et demanarà la
contrasenya en entrar amb `#host`.

### La primera vegada: "Qui ets?"

En entrar com a professor, l'app et demana qui ets: tria el teu nom de la llista o
escriu-lo i prem **+ Afegir professor**. Queda recordat en aquest navegador, així que
els dies següents entres directe. Per canviar de professor, clica el botó **👤 amb el
teu nom** a dalt del panell.

Això només serveix per **ordenar el material per carpetes**, no és cap control
d'accés: tothom pot triar qualsevol carpeta i veure els quizzes dels altres.

---

## 2. El panell del professor

En entrar amb `#host` veus la llista de quizzes i, a dalt a la dreta:

- **📊 Historial** — partides ja acabades.
- **👥 Alumnes** — llistes de classe (4t A, 4t B…).
- **+ Nou quiz** — crear un qüestionari.

Cada quiz de la llista té: **▶ Jugar**, **⧉ Duplicar**, **✏️** (editar) i **🗑**.
A sota hi ha **Importar quiz (CSV / JSON)** i **⬇ Plantilla de quiz (CSV)**.

### Carpetes

Sota la barra hi ha els botons de carpeta: **📁 Els meus**, una carpeta per cada altre
professor amb material, **📁 Sense carpeta** (els quizzes d'abans que hi hagués
carpetes) i **Tots**. Comences sempre a la teva.

Dels quizzes d'un altre professor pots **▶ Jugar** i **⧉ Duplicar** (te'n fa una còpia
a la teva carpeta, per retocar-la sense tocar l'original). Editar i esborrar, només el
teu material.

---

## 3. Crear o editar un quiz

Dins l'editor: títol, temps per defecte de les preguntes noves i, si vols,
**🔀 aleatoritzar l'ordre de les opcions** per a cada alumne (dificulta copiar-se).

Per a cada pregunta pots triar:

- **Opció múltiple (mcq)** — 4 opcions, una de correcta.
- **Vertader / Fals (tf)** — 2 botons.
- **Resposta múltiple (multi)** — diverses opcions correctes (caselles ✓).
- **Escriure la resposta (fill)** — l'alumne escriu; tu indiques les respostes
  acceptades separades per `/` (p. ex. `London / londres`). No distingeix
  majúscules ni espais de més.

I també: **segons** d'aquella pregunta (10/20/30/40/60), **explicació** (es
projecta als resultats), **imatge** (URL, triant la variant "+ imatge" del tipus) i
la casella **×2** perquè la pregunta valgui el doble de punts.
Amb ↑ ↓ reordenes preguntes i amb **Eliminar** les esborres. No oblidis **💾 Desar**.

### Importar preguntes des d'un full de càlcul

Descarrega **⬇ Plantilla de quiz (CSV)**, omple-la i fes **⬆ Importar quiz (CSV)**.
Columnes: `pregunta, opcioA, opcioB, opcioC, opcioD, correcta, segons, explicacio, tipus, imatge`.
A `correcta` pots posar `A-D`, `1-4`, `True/False` o diverses lletres (`A,C`) per a
respostes múltiples; a `tipus`, `mcq`, `tf`, `multi` o `fill`.

---

## 4. Llistes de classe (👥 Alumnes)

Crea una llista per classe i enganxa-hi els alumnes, **un per línia amb nom i
cognom** (pots copiar una columna de Google Sheets) o importa un CSV d'una sola
columna. Serveix per validar qui entra: si tries una classe en llançar la partida,
només hi poden entrar els noms d'aquesta llista.

L'app és tolerant amb com escriuen el nom: accepta el nom de pila si és únic i, si
hi ha dos "Marc", li fa triar entre "Marc Vila" i "Marc Puig".

---

## 5. Jugar una partida

1. **▶ Jugar** al quiz → tria **quina classe hi juga** (o *Sense validació ·
   qualsevol nom* si vols deixar entrar a tothom).
2. Surt el **PIN de 4 xifres** i l'adreça. Projecta aquesta pantalla: els noms dels
   alumnes van apareixent a mesura que entren (pots expulsar-ne un clicant-hi).
3. **Començar el joc ▶** quan hi siguin tots.
4. Per a cada pregunta veus el compte enrere i quants han respost. Tens
   **⏸ Pausa**, **+10 s** i **Tancar i veure resultats →**. La pregunta es tanca
   sola quan s'acaba el temps o quan han respost tots.
5. A la pantalla de resultats: gràfic de respostes, explicació, classificació,
   **👁 Veure resposta de cada alumne** i **← Pregunta anterior** per repassar-ne
   una de feta (no es torna a puntuar).
6. Al final: podi, **🔄 Jugar de nou**, i les descàrregues de resultats.

**Puntuació:** resposta immediata ≈ 1000 punts, al límit del temps ≈ 500,
incorrecta o en blanc 0; les preguntes ×2 valen el doble. A part dels punts,
l'app calcula una **nota sobre 10** = encerts / total × 10, que és la que surt als CSV.

---

## 6. Resultats i historial

Al final de la partida pots descarregar:

- **⬇ Classificació (CSV)** — Posició, Nom, Encerts, Nota (/10), Punts.
- **⬇ Respostes completes (CSV)** — una columna per pregunta amb què va contestar
  cadascú, més Encerts / Nota / Punts.

Els CSV s'obren bé a Excel (accents inclosos). Tota partida acabada queda desada a
**📊 Historial**, on la pots tornar a descarregar (**⬇ CSV**) o esborrar (**🗑**).
L'historial et mostra **les teves partides**; el botó **Veure les de tothom** obre les
de la resta de professors (les pots descarregar, però no esborrar).

---

## 7. Coses a tenir en compte

- **La pantalla del professor mana**: si tanques la pestanya enmig d'una partida,
  la partida es queda penjada. Els alumnes sí que es poden reconnectar si recarreguen.
- Les partides en directe s'esborren soles passades **12 h**; l'historial no es toca.
- **Diversos professors alhora, sense problema**: cada partida reserva un PIN lliure,
  així dues classes jugant a la mateixa hora no es poden trepitjar.
- Els alumnes **no reben mai la resposta correcta** per la xarxa, però la seguretat
  és la d'una aula: qui tingui l'enllaç i el PIN pot entrar. No és un examen blindat.
- Actualitzar el fitxer `index.html` **no esborra dades**: són a Firebase.
