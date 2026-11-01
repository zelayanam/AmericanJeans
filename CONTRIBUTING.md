# Cómo colaborar — American Jeans

Guía corta para trabajar sobre este repositorio sin pisar el trabajo de otros.
Se hace desde Windows, con Git Bash o MSYS2 UCRT64.

---

## Los dos remotes

| Remote | Apunta a | Permiso |
|---|---|---|
| `origin` | tu fork — `github.com/zelayanam/AmericanJeans` | lectura y escritura |
| `upstream` | el original — `github.com/DaniP2021/AmericaJeans` | solo lectura |

Los cambios **no** se hacen sobre `main` del original ni se commitean directo a `main`.
Van en una rama de `origin` y llegan al original por Pull Request.

---

## Puesta en marcha (una sola vez por máquina)

```bash
git clone https://github.com/zelayanam/AmericanJeans.git
cd AmericanJeans
git remote add upstream https://github.com/DaniP2021/AmericaJeans.git
git remote -v
```

Tiene que mostrar `origin` con tu usuario y `upstream` con `DaniP2021`.

Identidad, si todavía no está configurada:

```bash
git config --global user.name "zelayanam"
git config --global user.email "zelayanam@gmail.com"
```

---

## Ciclo de trabajo

```bash
# 1. partir de main actualizado
git switch main
git pull origin main

# 2. crear la rama del trabajo
git switch -c docs/mi-cambio

# 3. trabajar, y ver qué cambió
git status
git diff

# 4. commit
git add CONTRIBUTING.md
git commit -m "Documenta el flujo de trabajo del repositorio"

# 5. subir la rama al fork
git push -u origin docs/mi-cambio
```

Después, en GitHub: aparece un botón **Compare & pull request** sobre tu fork.
Base del PR: `DaniP2021/AmericaJeans:main`. Cabeza: `zelayanam/AmericanJeans:docs/mi-cambio`.

---

## Nombres de rama

| Prefijo | Para |
|---|---|
| `feat/` | funcionalidad nueva |
| `fix/` | corrección de un error |
| `docs/` | documentación |
| `chore/` | mantenimiento, configuración, limpieza |

En minúsculas, con guiones: `fix/precio-talle-44`, no `FixPrecio44`.

---

## Mensajes de commit

En español, en imperativo, primera línea de hasta 72 caracteres y sin punto final.
Si hace falta contexto, se agrega después de una línea en blanco.

```
Agrega tabla de precios de la línea basic

Precios de lista sin IVA discriminado. Falta revisar los de jean.
```

Referencias al estilo que ya usa el repo:

```
Agrega arranque automatico para trabajar desde cualquier PC
Catalogo American Jeans: 18 productos, herramienta de fotos y documentacion
```

---

## Mantenerse al día con el original

El trabajo de otros llega a `upstream`, no a tu fork. Antes de abrir un PR:

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

Si `main` de tu fork quedó atrasado mientras trabajabas en una rama, conviene
traer los cambios a la rama antes de pedir el merge:

```bash
git switch docs/mi-cambio
git merge main
```

---

## Qué no se sube

El `.gitignore` ya excluye lo que no corresponde versionar: fotos crudas,
entornos virtuales, temporales de Windows y modelos pesados. No se fuerza con
`git add -f` sin hablarlo antes.

Los archivos de `CATALOGO/` se regeneran con los scripts de
`arquitectura-agente-tienda/`; no se editan a mano.

---

## Licencia

El repositorio no tiene archivo `LICENSE`: queda con copyright por defecto de sus
autores. Se puede usar y modificar en el marco de este proyecto; para publicar
una copia propia o reutilizar el material fuera de él, hay que consultar antes
con el dueño del repositorio.
