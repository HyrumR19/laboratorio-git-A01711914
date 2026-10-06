# Mi cheatsheet de git y terminal

## Primero: ubicarme en la terminal

| Comando | Cómo lo explico |
| ------- | --------------- |
| `pwd` | Me dice en qué carpeta estoy parado. Si algo falla, es lo primero que reviso. |
| `ls` | Me enseña qué hay en esa carpeta.|
| `cd carpeta` | Me mete a esa carpeta. `cd ..` me saca un nivel y `cd ~` me regresa a mi carpeta de usuario. |
| `mkdir -p a/b/c` | Crea carpetas, y con `-p` crea toda la cadena de un jalón. |

Truco: Tab autocompleta nombres. Si Tab no completa nada, ese archivo o carpeta no existe donde estoy.

## Los tres lugares donde puede estar un cambio

1. **Mi carpeta** (working directory): lo que edito en VS Code.
2. **La caja de preparación** (staging): lo que ya escogí para el siguiente commit.
3. **El historial** (commits): lo que ya quedó guardado.

## Comandos del día a día

**`git status`**
Es como preguntarle a Git "¿cómo va todo?". Me dice en qué rama estoy, qué archivos cambié, cuáles ya metí a la caja y cuáles Git ni siquiera conoce (untracked).

**`git add archivo`** (o `git add .` para todo)
Mete el cambio a la caja de preparación. Ojo: guarda una *foto* del archivo en ese momento. Si después lo vuelvo a editar, tengo que hacer `git add` otra vez o el cambio nuevo no entra al commit.

**`git commit -m "Mensaje"`**
Cierra la caja y la guarda en el historial con un mensaje. Solo se queda en mi computadora. El mensaje empieza con un verbo en presente y dice qué cambió, por ejemplo: "Agrega tabla de herramientas al README".

**`git push`**
Sube a GitHub todos los commits que tengo y que GitHub todavía no tiene. Si me lo rechaza es porque alguien subió algo antes: hago `git pull --no-edit` y luego vuelvo a hacer `git push`.

**`git pull`**
Baja lo que mis compañeros subieron y lo junta con lo mío. Regla de oro: **siempre antes de empezar a trabajar y antes de subir.**

**`git log`** (yo uso `git log --oneline`)
Me enseña la lista de commits, del más nuevo al más viejo. Con `--oneline` sale uno por renglón y es más fácil de leer. Con `--graph --all` me dibuja las ramas.

**`git diff`**
Me dice qué cambié en mis archivos **desde el último `git add`**, o sea, lo que todavía no está en la caja.

**`git diff --staged`**
Me dice qué hay **dentro de la caja** comparado con el último commit, o sea, exactamente lo que entraría si hago commit ahorita.

## Para deshacer

**`git restore archivo`**
Regresa el archivo a como estaba en el último commit. Sirve para dos cosas: tirar cambios que no me gustaron (y esos **se pierden para siempre**, porque nunca se guardaron) o recuperar un archivo que borré sin querer.

**`git restore --staged archivo`**
Saca el archivo de la caja de preparación pero **no toca lo que escribí**. Es para cuando hice `git add` de algo que no quería subir todavía.

> La diferencia en una frase: `--staged` saca de la caja y conserva; sin `--staged` borra mis cambios.

**`git commit --amend -m "Mensaje bueno"`**
Corrige el último commit (por ejemplo, un mensaje mal escrito). Solo si **todavía no hice push**; si ya lo subí, mejor hago un commit nuevo.

## Mini tabla para decidir

| Me pasó esto | Uso | ¿Qué pasa con mi trabajo? |
| ------------ | --- | ------------------------- |
| Edité y me arrepentí, sin `add` | `git restore archivo` | Se pierde |
| Hice `add` de algo que no quería | `git restore --staged archivo` | Se conserva |
| Borré un archivo por accidente | `git restore archivo` | Se recupera |
| Mensaje de commit mal (sin subir) | `git commit --amend -m "..."` | Se conserva |
| Quiero ver antes de decidir | `git diff` / `git diff --staged` | No se toca |

## Cosas que aprendí a la mala

- Casi todos los errores son de ubicación: el comando está bien pero lo corrí en la carpeta equivocada. `pwd` y `ls` antes de todo.
- Git sí guarda archivos vacíos, pero **no** carpetas vacías. Por eso cada carpeta lleva un `README.md`.
- Nunca hacer `git init` dentro de una carpeta que ya es repositorio.
