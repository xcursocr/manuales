# 🐙 GitHub: Guía Práctica para Subir Proyectos y Trabajar en Equipo

## 📦 1. Inicializar y Subir un Proyecto Nuevo

```bash
# Dentro de tu carpeta de proyecto
git init                            # Inicia el repositorio local
git add .                           # Agrega todos los archivos
git commit -m "Primer commit"       # Crea el primer commit

# Conecta tu proyecto con GitHub
git remote add origin https://github.com/usuario/repositorio.git

# Sube tu código al repositorio (main o master según tu caso)
git branch -M main                  # (opcional) Renombra la rama a main
git push -u origin main             # Sube el código a GitHub

```

## 📦 2. Subir Cambios al Repositorio

```bash
git add .                           # Agrega cambios (puede usar archivos específicos)
git commit -m "Descripción del cambio"
git push                            # Sube al repositorio remoto

```
## 📦 3. Crear y Usar Ramas (branches)

```bash
git checkout -b nueva-rama          # Crea y cambia a nueva rama
# Realiza cambios y súbelos
git add .
git commit -m "Cambios en nueva rama"
git push -u origin nueva-rama       # Sube la nueva rama al remoto

```
## 📦 4. Cambiar de Rama

```bash
git checkout main                   # Cambia de rama
git pull                            # Actualiza la rama local desde GitHub

```
## 📦 5. Trabajar en 2 PCs con un Repositorio

```bash
git clone https://github.com/usuario/repositorio.git

# **Cada vez que cambies de PC:**
git pull                            # Descarga los últimos cambios
# Haz tus cambios
git add .
git commit -m "Cambios desde PC2"
git push                            # Sube tus cambios


```
⚔️ 6. Fusionar Ramas (merge)

```bash
git checkout main
git pull
git merge nueva-rama                # Une la rama al main
git push                            # Sube la fusión

```
⚔️ ⚠️ 7. Resolver Conflictos
Si hay conflicto al hacer merge o pull:
1. Git te mostrará los archivos en conflicto.
2. Edita manualmente el contenido (busca <<<<<<<).
3. Luego:

```bash
git add archivo-resuelto
git commit -m "Conflicto resuelto"
git push

```
📁 8. Ignorar Archivos con .gitignore

```bash
node_modules/
.env
.DS_Store
```

🔄 9. Sincronizar Forks (avanzado)

```bash
git remote add upstream https://github.com/original/repositorio.git
git fetch upstream
git merge upstream/main
```

🧠 Recomendaciones Finales
1. Usa ramas para nuevas funcionalidades.
2. Haz pull antes de trabajar.
3. Usa .gitignore siempre.
4. Commits pequeños y frecuentes = mejor historial.
5. No subas claves ni tokens (usa .env).

✅ Recursos Recomendados
1. [GitHub Docs](https://docs.github.com/es)
2. [Pro Git Book](https://git-scm.com/book/en/v2)
3. [gitignore.io](https://www.toptal.com/developers/gitignore/)
