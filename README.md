
# Despliegue en Pythonanywhere.com

```
pa_autoconfigure_django.py --python=3.12 https://github.com/juandtap/djangogirlstutorial
```
Nota. En el ambiente de pythonanywhere trabajan con la version 3.12 o 3.13 si se usa otras antiguas o mas recientes lanza error en la consola

# 🔑 Guía de Configuración e Inicio con SSH para GitHub

Este repositorio incluye una guía rápida para configurar tu autenticación mediante **claves SSH** en GitHub. Usar SSH en lugar de HTTPS te permite hacer `git push` y `git pull` de forma segura sin tener que ingresar tu usuario y token/contraseña en cada ocasión.

---

## 📋 Requisitos Previos

Asegúrate de tener **Git** instalado en tu sistema:
* **Linux:** `git --version` (Instalar vía gestor de paquetes ej. `sudo apt install git`)
* **Windows:** Instalar [Git for Windows](https://gitforwindows.org/) (incluye **Git Bash**).

---

## 🐧 Configuración en Linux

Abre tu terminal y sigue estos pasos:

### 1. Generar la clave SSH
Ejecuta el siguiente comando (reemplaza con el correo asociado a tu cuenta de GitHub):

```bash
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```
Presiona Enter para aceptar la ubicación por defecto y asigna una contraseña (passphrase) opcional si deseas mayor seguridad.

### 2. Iniciar el agente SSH y agregar la clave

```# Iniciar el agente SSH en segundo plano
eval "$(ssh-agent -s)"
```
```
# Agregar tu clave privada al agente
ssh-add ~/.ssh/id_ed25519
```

### 3. Copiar la clave pública para GitHub
Muestra el contenido de tu clave pública y cópialo completo:

```
cat ~/.ssh/id_ed25519.pub
```

## 🪟 Configuración en Windows
Abre Git Bash (incluido con Git for Windows) o PowerShell y sigue estos pasos:

### 1. Generar la clave SSH
```
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```
Presiona Enter para aceptar la ruta predeterminada (C:\Users\TuUsuario\.ssh\id_ed25519).

### 2. Iniciar el servicio SSH y agregar la clave
En Git Bash:
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

En PowerShell (Como Administrador):

PowerShell
```
# Asegurar que el servicio ssh-agent esté activo
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent

# Agregar la clave
ssh-add ~$env:USERPROFILE\.ssh\id_ed25519

```
### 3. Copiar la clave pública para GitHub
En Git Bash:
```
cat ~/.ssh/id_ed25519.pub
```

En PowerShell:

```
Get-Content ~$env:USERPROFILE\.ssh\id_ed25519.pub

```

## 🌐 Agregar la Clave Pública a GitHub
Copia todo el texto generado por el comando cat o Get-Content (comienza con ssh-ed25519 ...).

Ve a tu cuenta de GitHub ➔ Settings (Configuración) ➔ SSH and GPG keys.

Haz clic en New SSH key.

Asigna un Title (ej. Laptop Trabajo, PC Escritorio Linux/Win).

En el campo Key, pega tu clave pública.

Haz clic en Add SSH key.

## ✅ Comprobar la Conexión
Para verificar que la clave esté configurada correctamente, ejecuta el siguiente comando en tu terminal (Linux/Git Bash/PowerShell):

```
ssh -T git@github.com
```
Si todo es correcto, verás un mensaje similar a este:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```


## 🚀 Clonar este Repositorio mediante SSH
Una vez configurado, clona este repositorio usando la URL SSH:

```
git clone git@github.com:usuario/nombre-del-repositorio.git
```

Si ya habías clonado el repositorio mediante HTTPS, puedes cambiar la URL a SSH con:

```
git remote set-url origin git@github.com:usuario/nombre-del-repositorio.git
```

