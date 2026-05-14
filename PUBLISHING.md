# Publicar el sitio en GitHub Pages

Estas instrucciones te llevan desde la carpeta local hasta tener
`https://dalmonacid-a.github.io/` en línea. Cada bloque de comandos se
ejecuta en la **Terminal de tu Mac**, no en el sandbox.

---

## 0. Requisitos previos

Verifica que tienes Git instalado abriendo Terminal y ejecutando:

```bash
git --version
```

Si no aparece la versión, instala las herramientas de desarrollo de Apple:

```bash
xcode-select --install
```

Acepta el cuadro de diálogo y espera a que termine (unos minutos).

Verifica también que tienes una cuenta en https://github.com con el
usuario `dalmonacid-a` (si todavía no existe, créala antes de seguir y
confirma el correo).

---

## 1. Limpiar el repositorio Git que quedó a medias

Durante la preparación se creó un directorio `.git/` parcial dentro de tu
carpeta del sitio. Bórralo desde tu Terminal:

```bash
cd ~/Documents/Codex/2026-05-08/files-mentioned-by-the-user-almonacid/academicpages-site
rm -rf .git
```

> Si Terminal te pide confirmación, escribe `y` y presiona Enter.

---

## 2. Configurar Git (solo la primera vez)

```bash
git config --global user.name "Diego Almonacid-Almarza"
git config --global user.email "dalmonacid.a@gmail.com"
git config --global init.defaultBranch main
```

---

## 3. Inicializar el repositorio y hacer el primer commit

Desde la misma carpeta del sitio:

```bash
git init
git add -A
git commit -m "Initial commit: personalized academicpages site"
```

El `.gitignore` ya está configurado, así que `vendor/`, `_site/`,
`node_modules`, `.bundle`, `.sass-cache` y `Gemfile.lock` quedan fuera
del commit automáticamente.

---

## 4. Crear el repositorio remoto en GitHub

1. Inicia sesión en https://github.com con la cuenta `dalmonacid-a`.
2. Haz clic en el botón **+** arriba a la derecha → **New repository**.
3. En **Repository name** escribe exactamente:

   ```
   dalmonacid-a.github.io
   ```

   (Este nombre especial hace que el sitio se sirva en la raíz del
   subdominio.)

4. Selecciona **Public**.
5. **Importante:** no marques "Add a README", ni `.gitignore`, ni
   licencia. Tu carpeta local ya tiene esos archivos y queremos evitar
   conflictos.
6. Pulsa **Create repository**.

---

## 5. Conectar tu carpeta local con GitHub y subirla

GitHub te mostrará un bloque de comandos. Usa estos (sustitúyelos por
los que ves en pantalla solo si difieren):

```bash
git remote add origin https://github.com/dalmonacid-a/dalmonacid-a.github.io.git
git branch -M main
git push -u origin main
```

La primera vez que hagas `git push`, macOS abrirá una ventana del
navegador para autenticarte en GitHub. Acepta el inicio de sesión.

> Si más adelante prefieres no introducir credenciales cada vez,
> instala GitHub CLI con `brew install gh` y ejecuta `gh auth login`.

---

## 6. Activar GitHub Pages

1. En la página de tu nuevo repositorio en GitHub, entra en
   **Settings** → **Pages** (en la barra lateral izquierda).
2. En **Source**, selecciona:
   - Branch: `main`
   - Folder: `/ (root)`
3. Pulsa **Save**.
4. Espera 1-2 minutos. Cuando el primer build termine, GitHub mostrará
   un cuadro verde con tu URL:

   ```
   https://dalmonacid-a.github.io/
   ```

5. Puedes ver el progreso del build en la pestaña **Actions** del
   repositorio.

---

## 7. Conectar un dominio personal (más adelante)

Cuando quieras usar un dominio propio (por ejemplo `almonacid.legal`):

1. Compra el dominio en un registrador (Namecheap, Cloudflare, Porkbun).
2. En **Settings → Pages → Custom domain**, escribe el dominio y guarda.
   GitHub creará un archivo `CNAME` en el repositorio.
3. En el panel DNS de tu registrador, añade los registros que GitHub
   indica:
   - 4 registros `A` apuntando a las IPs de GitHub Pages, **o**
   - un `CNAME` que apunte a `dalmonacid-a.github.io` (si usas un
     subdominio como `www.almonacid.legal`).
4. Marca **Enforce HTTPS** una vez que el certificado se haya emitido
   (suele tardar unas horas).

---

## Flujo de trabajo cotidiano

A partir de aquí, para publicar cualquier cambio:

```bash
cd ~/Documents/Codex/2026-05-08/files-mentioned-by-the-user-almonacid/academicpages-site
# Edita los archivos que quieras
git add -A
git commit -m "Descripción breve del cambio"
git push
```

GitHub Pages reconstruye y publica automáticamente en 1-2 minutos.

---

## Vista previa local (opcional)

Para ver el sitio antes de publicar, en Terminal:

```bash
cd ~/Documents/Codex/2026-05-08/files-mentioned-by-the-user-almonacid/academicpages-site
brew install ruby node
gem install bundler
bundle install
bundle exec jekyll serve -l -H localhost
```

Después abre http://localhost:4000 en el navegador. Para detenerlo,
`Ctrl+C` en la Terminal.

---

## Cambios ya aplicados en tu carpeta

Para que sepas qué se modificó:

- `_config.yml`: añadidos `url`, `repository` y `author.github`.
- `_data/authors.yml`: reemplazadas las entradas dummy por una entrada
  tuya.
- `_drafts/post-draft.md`: marcado como `published: false`.
- `_pages/markdown.md`, `terms.md`, `archive-layout-with-content.md`,
  `non-menu-page.md`, `cv-json.md`: marcados como `published: false`
  para que no aparezcan en el sitio público.
- `.gitignore`: ya estaba bien configurado, no se tocó.
