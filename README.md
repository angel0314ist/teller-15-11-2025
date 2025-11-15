# Ejemplo práctico: Ciclo CI/CD hasta la construcción del PACKAGE (Node.js)

**Repositorio:** [https://github.com/angel0314ist/teller-15-11-2025](https://github.com/angel0314ist/teller-15-11-2025)

**Objetivo:** Proveer un repositorio completo que demuestre un pipeline CI/CD (GitHub Actions) que:

1. Ejecuta pruebas unitarias.
2. Construye/empaca el package (`npm pack`).
3. Publica un artefacto (`package.tgz`) desde el pipeline.

---

## Estructura del repositorio

```
/
├─ .github/
│  └─ workflows/
│     └─ ci.yml
├─ src/
│  └─ index.js
├─ tests/
│  └─ index.test.js
├─ package.json
├─ .gitignore
└─ README.md
```

---

## Contenido clave

* **README.md**: Explicación del flujo CI/CD y pasos reproducibles.
* **.github/workflows/ci.yml**: Workflow que instala dependencias, ejecuta pruebas (Jest), genera el package y sube el artefacto.
* **tests/index.test.js**: Prueba unitaria simple.
* **package.json**: Contiene los scripts `test` y `pack`.

---

## Flujo CI/CD explicado paso a paso

1. Realizas un **commit/push** a la rama `main` o abres un Pull Request.
2. GitHub Actions detecta el evento (`push` o `pull_request`).
3. El runner ejecuta:

   * `actions/checkout@v4` → obtiene el código.
   * Instalación de Node.js.
   * `npm ci` o `npm install`.
   * `npm test` (si falla, el pipeline se detiene).
   * `npm pack` → genera un archivo `.tgz`.
   * Sube el artefacto generado.
4. El artefacto se puede descargar desde la pestaña **Actions**.

---

## Cómo reproducir localmente

1. Clona tu repositorio:

```bash
git clone https://github.com/angel0314ist/teller-15-11-2025.git
cd teller-15-11-2025
```

2. Instala dependencias:

```bash
npm install
```

3. Ejecuta pruebas:

```bash
npm test
```

4. Empaca el proyecto:

```bash
npm pack
```

Esto generará un archivo `.tgz`, por ejemplo: `teller-15-11-2025-1.0.0.tgz`.

---

## Archivo de workflow (GitHub Actions)

Este archivo se encuentra en `.github/workflows/ci.yml`.

Eventos:

* `push` y `pull_request` sobre `main`.

El job incluye:

* `actions/checkout@v4`.
* `actions/setup-node@v4`.
* Instalación de dependencias.
* Ejecución de pruebas.
* Construcción del package con `npm pack`.
* Subida del artefacto usando `actions/upload-artifact@v4`.

Al finalizar, en **Actions** aparecerá el archivo generado listo para descargar.

---

## Ejemplo de pruebas incluidas

`tests/index.test.js` contiene una prueba simple:

* Verifica que la función `sum(a, b)` retorna la suma correcta.

---

## Mapeo con la rúbrica de evaluación

1. **README.md** — documentación clara y reproducible.
2. **Configuración CI/CD** — archivo de workflow funcional.
3. **Pruebas** — pruebas unitarias funcionando con Jest.
4. **Construcción del package** — uso de `npm pack` y generación de artefacto.
5. **Repositorio público** — el repositorio en GitHub está accesible.

---

## Notas finales y buenas prácticas

* Considera proteger la rama `main` para requerir CI exitoso antes de hacer merge.
* Puedes añadir versionado semántico y releases automáticos.
* Para publicar en npm, agrega un `NPM_TOKEN` seguro como secret.

---

Autor: **Angel Quishpe**
Fecha: *15/11/2025*
