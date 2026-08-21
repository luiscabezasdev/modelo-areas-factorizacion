# Guía: subir tu proyecto a Git y publicarlo con tu dominio

Esta guía asume que ya tienes **Git instalado** y una **cuenta de GitHub**. Vamos a subir `index.html` (tu simulador de factorización) a un repositorio, activar GitHub Pages y conectarlo con el dominio que ya tienes.

Todos los comandos se ejecutan en la terminal (PowerShell, CMD o Git Bash) dentro de la carpeta `Calculo_Integral`.

## 1. Crear el repositorio en GitHub

1. Entra a [github.com](https://github.com) y da clic en **New repository** (el botón `+` arriba a la derecha → *New repository*).
2. Ponle un nombre, por ejemplo `modelo-areas-factorizacion`.
3. Déjalo en **Public** (necesario para usar GitHub Pages gratis).
4. **No** marques "Add a README" ni ".gitignore" (ya los tenemos localmente).
5. Da clic en **Create repository**. GitHub te va a mostrar una URL como:
   `https://github.com/TU-USUARIO/modelo-areas-factorizacion.git`
   Guárdala, la usas en el paso 3.

## 2. Inicializar Git en tu carpeta local

Abre una terminal en la carpeta `Calculo_Integral` (la que tiene `index.html` y `README.md`) y ejecuta:

```bash
git init
git add .
git commit -m "Primera versión: modelo de áreas para factorización"
```

Esto crea el repositorio local, agrega tus archivos y hace el primer commit.

> Si es la primera vez que usas Git en esta computadora, puede pedirte configurar tu identidad:
> ```bash
> git config --global user.name "Tu Nombre"
> git config --global user.email "tu-correo@ejemplo.com"
> ```

## 3. Conectar con GitHub y subir (push)

```bash
git branch -M main
git remote add origin https://github.com/TU-USUARIO/modelo-areas-factorizacion.git
git push -u origin main
```

Te pedirá iniciar sesión (usuario y token, o se abrirá el navegador si tienes GitHub CLI/Git Credential Manager). Cuando termine, recarga la página del repositorio en GitHub y deberías ver tus archivos.

## 4. Activar GitHub Pages

1. En tu repositorio en GitHub, ve a **Settings** → **Pages** (menú izquierdo).
2. En **Source**, selecciona la rama `main` y la carpeta `/ (root)`.
3. Guarda. En unos segundos GitHub te dará una URL tipo:
   `https://TU-USUARIO.github.io/modelo-areas-factorizacion/`
4. Abre esa URL para confirmar que tu simulador carga correctamente.

## 5. Conectar tu dominio propio

Aquí hay dos formas de usar tu dominio. Elige según lo que quieras:

- **Dominio raíz** (`tudominio.com`) → necesitas registros **A**.
- **Subdominio** (`www.tudominio.com` o `proyectos.tudominio.com`) → necesitas un registro **CNAME**. Es más simple y GitHub lo recomienda.

### 5a. En GitHub

1. En **Settings → Pages**, en el campo **Custom domain**, escribe tu dominio (ej. `www.tudominio.com` o `tudominio.com`) y guarda.
2. Esto crea automáticamente un archivo `CNAME` en tu repositorio con ese dominio adentro. Después de guardar, baja los cambios a tu copia local:
   ```bash
   git pull
   ```

### 5b. En el panel de tu proveedor de dominio (donde compraste el dominio)

Busca la sección **DNS** (a veces dice "Administrar DNS" o "Zone editor") y agrega:

**Si usas subdominio (recomendado, ej. `www`):**

| Tipo  | Host/Nombre | Valor                        |
|-------|-------------|-------------------------------|
| CNAME | www         | `TU-USUARIO.github.io`        |

**Si usas dominio raíz (`tudominio.com` sin `www`):**

Agrega 4 registros tipo **A** apuntando todos a las IPs de GitHub Pages:

| Tipo | Host/Nombre | Valor           |
|------|-------------|-----------------|
| A    | @           | 185.199.108.153 |
| A    | @           | 185.199.109.153 |
| A    | @           | 185.199.110.153 |
| A    | @           | 185.199.111.153 |

> Tip: mucha gente configura ambos — el dominio raíz con registros A, y `www` con CNAME apuntando a `TU-USUARIO.github.io` — así funcionan las dos formas de escribir la URL.

Los cambios de DNS pueden tardar desde minutos hasta un par de horas en propagarse.

## 6. Verificar y activar HTTPS

1. Vuelve a **Settings → Pages** en GitHub.
2. Cuando el DNS ya propagó, verás una marca de verificación junto a tu dominio.
3. Marca la casilla **Enforce HTTPS** para que tu sitio use `https://` de forma segura.

## 7. Cómo actualizar el sitio en el futuro

Cada vez que edites `index.html` (por ejemplo, agregando nuevas funciones al simulador):

```bash
git add .
git commit -m "Describe aquí qué cambiaste"
git push
```

GitHub Pages se actualiza automáticamente en 1-2 minutos después del push.

---

### Resumen rápido de comandos (primera vez)

```bash
git init
git add .
git commit -m "Primera versión"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/TU-REPO.git
git push -u origin main
```

Luego: Settings → Pages → activar → poner dominio → configurar DNS → Enforce HTTPS.
