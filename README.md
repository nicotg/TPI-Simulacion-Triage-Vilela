# TPI Simulación — Guardia del Hospital Vilela

Informe del Trabajo Práctico Integrador de Simulación: modelo de la guardia
de emergencias pediátricas del Hospital de Niños Víctor J. Vilela, construido
en AnyLogic.

## Qué hay acá

| Archivo | Qué es |
| --- | --- |
| `informe.tex` | Documento principal. Sólo preámbulo, portada y los `\input` de cada sección. |
| `secciones/` | Una sección por archivo. **Acá se escribe.** |
| `arxiv.sty` | Estilo del template de preprints. No se toca. |
| `plano_guardia_vilela.png` | Plano de la guardia, figura 1. |
| `.github/workflows/` | Compila el PDF en cada push. |

El informe sigue los diez pasos de un estudio de simulación. Cada paso es un
archivo en `secciones/`, numerado en el orden en que aparece.

## Cómo conseguir el PDF

**Sin instalar nada.** Cada vez que alguien hace push, GitHub compila el
informe solo. Para bajarlo: pestaña **Actions** → la corrida más reciente →
abajo de todo, **Artifacts** → `informe`.

Si la corrida aparece con una cruz roja, el documento no compila. Entrá a la
corrida y buscá la línea que empieza con `!`: ahí está el error.

**Compilando en tu máquina.** Requiere TeX Live o MiKTeX instalado.

```bash
pdflatex informe.tex
pdflatex informe.tex   # la segunda pasada arma el índice
```

**En Overleaf.** Proyecto nuevo en blanco y subir todos los archivos
respetando la carpeta `secciones/`.

## Cómo editar sin pisarse

Somos varios escribiendo el mismo documento. Tres reglas que evitan casi
todos los conflictos:

**1. Cada uno en su archivo.** Antes de empezar, avisen qué sección van a
tocar. Dos personas en el mismo archivo es la única forma de generar
conflictos serios.

**2. Una oración por línea.** Suena raro, pero es la práctica estándar para
escribir LaTeX entre varios:

```latex
El modelo representa el recorrido completo del paciente.
Los pacientes ingresan de manera peatonal o en ambulancia.
```

y no así:

```latex
El modelo representa el recorrido completo del paciente. Los pacientes
ingresan de manera peatonal o en ambulancia.
```

El PDF sale idéntico, porque LaTeX ignora los saltos de línea simples. La
diferencia es que si alguien agrega tres palabras al principio de un párrafo
escrito a lo ancho, se recorta todo y git marca el párrafo entero como
modificado. Con una oración por línea, un cambio toca una línea.

El texto que ya está viene cortado por ancho, no por oración. No hace falta
convertirlo de una: aplicá la regla a lo que escribas de nuevo.

**3. No versionar el PDF.** Está en el `.gitignore`. Es binario y genera
conflictos que no se pueden resolver.

## Flujo de trabajo

```bash
git pull                          # siempre antes de empezar
git checkout -b seccion-5         # una rama por tarea
# ... editar ...
git add secciones/05-ejecuciones-piloto.tex
git commit -m "Completa resultados de las ejecuciones piloto"
git push -u origin seccion-5
```

Después, merge a `main` desde GitHub. Para cuatro personas con fecha de
entrega no hace falta formalizar pull requests: alcanza con ramas y avisarse.

## Lo que falta

El documento tiene **marcadores `[PENDIENTE]` en rojo** señalando cada
decisión que el grupo todavía debe tomar o cada resultado que falta cargar.
Para encontrarlos todos:

```bash
grep -rn "begin{pendiente}" secciones/
```

Los principales:

- Nombres, legajos y correos de los integrantes (en el preámbulo de
  `informe.tex`).
- Tasa de arribos: constante o variable por franja horaria.
- Proporción de pacientes de código rojo: 1 % o 3 %.
- Probabilidad de internación del código naranja: 60 % o 85 %.
- Derivación a traumatología, radiografías y medicación.
- Resultados de las corridas de producción y el test de medias.
- Verificar edición y año de la bibliografía.

Cuando una decisión queda resuelta, se borra el bloque `\begin{pendiente}
... \end{pendiente}` completo.
