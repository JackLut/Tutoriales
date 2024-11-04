
# Conectar Git a GitHub en Windows 11

Este documento guía el proceso de conectar Git a GitHub usando una clave SSH en Windows 11. Asegúrate de sustituir cualquier texto entre paréntesis con la información específica para tu configuración.

---

### Paso 1: Configurar Git con tu información de usuario
Abre PowerShell como administrador y configura tu nombre y correo electrónico para Git. Esto se usará para identificar tus commits.

```bash
git config --global user.name "(NOMBRE)"
git config --global user.email "(CORREO)"
```

- **(NOMBRE)**: Cambia esto por tu nombre o nombre de usuario de GitHub.
- **(CORREO)**: Cambia esto por tu dirección de correo electrónico asociada a GitHub.

---

### Paso 2: Configurar el Servicio SSH
SSH es necesario para la autenticación segura con GitHub. Verifica si el servicio ssh-agent está activo.

```bash
Get-Service ssh-agent
```

Este comando muestra el estado actual del servicio `ssh-agent`. Si no está en ejecución, continúa con los pasos para configurarlo.

#### 2.1 Configurar el ssh-agent para iniciar manualmente

```bash
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
```

Esto configura el ssh-agent para iniciar manualmente cada vez que sea necesario.

---

### Paso 3: Iniciar el Servicio SSH
Inicia el servicio ssh-agent.

```bash
Start-Service ssh-agent
```

Esto habilita el agente SSH para almacenar tus claves SSH durante la sesión actual.

---

### Paso 4: Generar una Clave SSH
Ahora, crea una clave SSH en el formato `ed25519` para mejorar la seguridad.

1. Navega al directorio `.ssh` dentro de tu carpeta de usuario:

    ```bash
    cd C:\Users\(NOMBRE DEL EQUIPO)\.ssh
    ```

    - **(NOMBRE DEL EQUIPO)**: Sustituye esto con el nombre de tu computadora.

2. Ejecuta el comando para crear una nueva clave SSH:

    ```bash
    ssh-keygen -t ed25519 -C "(CORREO)"
    ```

    - **(CORREO)**: Ingresa el correo electrónico que usas para GitHub.

3. Cuando te solicite un archivo donde guardar la clave, presiona **Enter** para aceptar la ubicación predeterminada.

---

### Paso 5: Añadir la Clave SSH al ssh-agent
Después de generar la clave SSH, añade la clave privada al ssh-agent para la autenticación.

```bash
ssh-add id_ed25519
```

Este comando permite al ssh-agent manejar la clave para las conexiones SSH sin necesidad de introducir la contraseña cada vez.

---

### Paso 6: Copiar la Clave Pública
Para conectar GitHub, necesitarás añadir la clave pública en tu cuenta de GitHub.

1. Muestra la clave pública con el siguiente comando:

    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```

2. Copia la salida de este comando (la clave SSH pública) para usarla en el siguiente paso.

---

### Paso 7: Añadir la Clave SSH en GitHub
Ahora que tienes la clave pública copiada, ve a GitHub para vincularla a tu cuenta.

1. En GitHub, navega a **Settings > SSH and GPG keys**.
2. Haz clic en **New SSH key**.
3. Proporciona un título descriptivo (por ejemplo, "Clave SSH de Windows 11") para identificar esta clave en el futuro.
4. Pega tu clave pública en el campo **Key**.
5. Haz clic en **Add SSH key** para guardar la clave en GitHub.

---

¡Listo! Has configurado correctamente Git para conectar con GitHub a través de SSH en Windows 11.
