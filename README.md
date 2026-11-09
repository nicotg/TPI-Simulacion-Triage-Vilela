# TPI Simulación — Guardia del Hospital Vilela

Informe del Trabajo Práctico Integrador de Simulación: modelo de la guardia
de emergencias pediátricas del Hospital de Niños Víctor J. Vilela, construido
en AnyLogic.

## Qué hay acá

| Archivo | Qué es |
| --- | --- |
| `informe.tex` | El informe completo. **Acá se escribe.** |
| `arxiv.sty` | Estilo del template de preprints. No se toca. |
| `plano_guardia_vilela.png` | Plano de la guardia, figura 1. |
| `.github/workflows/` | Compila el PDF en cada push. |

El informe sigue los diez pasos de un estudio de simulación. Cada paso es una
sección numerada del documento, en orden.

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

**En Overleaf.** Proyecto nuevo en blanco y subir los cuatro archivos.

## Cómo editar

Todo el informe está en `informe.tex`. Dos cosas a tener en cuenta:

**Avisá qué sección vas a tocar.** Git fusiona solo los cambios que no se
superponen, así que dos personas trabajando en secciones distintas no se
pisan. El problema aparece cuando dos tocan el mismo párrafo.

**Hacé `git pull` antes de empezar y `git push` apenas termines.** Cuanto más
corto el ciclo, menos chance de superposición.

**No versiones el PDF.** Está en el `.gitignore`: es binario y genera
conflictos que no se pueden resolver.

## Flujo de trabajo

```bash
git pull                          # siempre antes de empezar
# ... editar informe.tex ...
git add informe.tex
git commit -m "Completa resultados de las ejecuciones piloto"
git push
```

Para cambios grandes conviene una rama:

```bash
git checkout -b analisis-resultados
# ... editar ...
git push -u origin analisis-resultados
```

y después merge a `main` desde GitHub.

## Lo que falta

El documento tiene **marcadores `[PENDIENTE]` en rojo** señalando cada
decisión que el grupo todavía debe tomar o cada resultado que falta cargar.
Para encontrarlos todos:

```bash
grep -n "begin{pendiente}" informe.tex
```

Los principales:

- Nombres, legajos y correos de los integrantes (en el preámbulo).
- Tasa de arribos: constante o variable por franja horaria.
- Proporción de pacientes de código rojo: 1 % o 3 %.
- Probabilidad de internación del código naranja: 60 % o 85 %.
- Derivación a traumatología, radiografías y medicación.
- Resultados de las corridas de producción y el test de medias.
- Verificar edición y año de la bibliografía.

Cuando una decisión queda resuelta, se borra el bloque `\begin{pendiente}
... \end{pendiente}` completo.
