# Formas Ternarias y Rondó

Guía de Estudio Interactiva sobre formas musicales ternarias y rondó.

## Seguridad y remediación de secretos

Este repositorio fue afectado por la exposición accidental de artefactos de Google API. A continuación se detallan los pasos de remediación recomendados.

### 1. Rotación y revocación de claves en Google Cloud Console

1. Ir a **Google Cloud Console** → **APIs & Services** → **Credentials** → **API keys**
2. Revocar las claves expuestas
3. Regenerar nuevas claves si es necesario

### 2. Restringir las claves API

Configurar restricciones para las nuevas claves:

- **Application restrictions (HTTP referrers):** Limitar a dominios autorizados
  - `https://josejolulu.github.io/*`
  - `https://josejolulu.github.io/Formas-Ternarias-y-Rondo/*`
- **API restrictions:** Seleccionar únicamente las APIs necesarias

### 3. Habilitar protecciones en GitHub

En **Settings** → **Code security and analysis**, habilitar:

- **Secret scanning**: Detecta secretos expuestos en el código
- **Push protection**: Bloquea commits que contienen secretos

### 4. Limpieza del historial de Git

Para purgar claves expuestas del historial, se pueden usar las siguientes herramientas:

#### Opción A: git filter-repo

```bash
git clone --mirror https://github.com/josejolulu/Formas-Ternarias-y-Rondo.git
cd Formas-Ternarias-y-Rondo.git

# Crear replacements.txt con las claves expuestas en formato:
# clave_expuesta==>REDACTED
git filter-repo --replace-text replacements.txt

git push --force --tags origin 'refs/heads/*'
```

#### Opción B: BFG Repo-Cleaner

```bash
# Usar un patrón regex para claves de Google API
bfg --replace-text <(echo 'regex:AIza[0-9A-Za-z-_]{35}==>REDACTED') repo.git
```

### 5. Marcar las alertas como resueltas

Una vez rotadas las claves y reescrita la historia de Git:

1. Ir a **Security** → **Secret scanning**
2. Marcar cada alerta como resuelta indicando que la clave fue revocada y el historial limpiado

---

© 2024 Educational Guide
