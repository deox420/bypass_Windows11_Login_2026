# How You Can Bypass Windows 11 Login (2026)

Esta guía detalla el proceso para saltarse la pantalla de inicio de sesión de Windows 11 y recuperar el acceso administrativo al sistema utilizando un USB de instalación. El método se basa en sustituir temporalmente el menú de accesibilidad por la consola de comandos.

> **Descargo de responsabilidad:** Esta guía es únicamente con fines educativos y de recuperación de sistemas propios. El uso de estas técnicas en equipos ajenos sin autorización es ilegal.

## 📋 Requisitos

* Un USB de instalación estándar de Windows 10/11 o un USB de arranque de utilidades (ej. Hiren’s Boot).
* Acceso físico al ordenador bloqueado.

---

## 🚀 Paso 1: Acceder a la consola de comandos (System Level)

1.  Conecta el USB y arranca el PC desde él (ajusta el orden de arranque en la BIOS si es necesario).
2.  Espera a que cargue la pantalla de instalación de Windows. **No pulses "Instalar" ni "Reparar".**
3.  Presiona la combinación de teclas:
    
    `Shift` + `F10`
    
4.  Se abrirá una ventana de comandos (`cmd.exe`) con privilegios de sistema.

---

## 🔄 Paso 2: El truco del "Cambiazo" (Swap)

Vamos a reemplazar el ejecutable del menú de accesibilidad (`utilman.exe`) por la consola de comandos (`cmd.exe`).

1.  En la consola, abre el Bloc de notas para usarlo como explorador de archivos visual:
    ```cmd
    notepad
    ```
2.  En el Bloc de notas, ve a **Archivo > Guardar como** (File > Save As).
3.  En la ventana de diálogo:
    * Cambia el tipo de archivo (abajo del todo) de *Documentos de texto (*.txt)* a **Todos los archivos (*.*)**.
    * Navega a: `Este equipo` > `Disco Local (C:)` > `Windows` > `System32`.
4.  Localiza los archivos y renómbralos en este orden:
    * Busca `utilman`. Haz clic derecho y renómbralo a `utilman1`.
    * Busca `cmd`. Haz clic derecho y renómbralo a `utilman`.
5.  Presiona `F5` para refrescar y asegurar que los nombres han cambiado.
6.  Cierra las ventanas del explorador y el Bloc de notas.
7.  En la consola negra, reinicia el equipo:
    ```cmd
    wpeutil reboot
    ```
    *(Retira el USB mientras se reinicia).*

---

## 🔓 Paso 3: Ejecución en la pantalla de bloqueo

1.  Deja que Windows cargue hasta la pantalla donde pide la contraseña.
2.  Haz clic en el **icono de Accesibilidad** (muñeco o silla de ruedas) situado en la esquina inferior derecha.
3.  En lugar de abrirse el menú de ayuda, se abrirá una consola de comandos (**CMD**) con permisos de `SYSTEM`.

---

## 🛠️ Paso 4: Soluciones según tu tipo de cuenta

Identifica si tu usuario es local o una cuenta de Microsoft (correo electrónico) y sigue la ruta adecuada.

### Opción A: Cuenta Local
Si usas un usuario tradicional (sin correo vinculado).

1.  Lista los usuarios para ver el nombre exacto:
    ```cmd
    net user
    ```
2.  Cambia la contraseña directamente:
    ```cmd
    net user "NombreDeTuUsuario" 1234
    ```
    * *Nota: Usa comillas si el nombre tiene espacios.*
    * *Reemplaza `1234` por la contraseña que quieras.*
3.  Cierra la consola e inicia sesión con la nueva contraseña.

### Opción B: Cuenta Microsoft (Email)
Si recibes el **Error 8646** al intentar cambiar la contraseña, usa este método.

1.  Crea un nuevo usuario local:
    ```cmd
    net user /add UsuarioAdmin 1234
    ```
2.  Otorga permisos de administrador al nuevo usuario:
    ```cmd
    net localgroup administrators /add UsuarioAdmin
    ```
3.  Reinicia el PC e inicia sesión con `UsuarioAdmin`.
4.  **Recuperar datos:** Como ahora eres admin, ve a `C:\Users\TuUsuarioAntiguo` desde el explorador de archivos y copia tus documentos, fotos y escritorio al nuevo perfil.

---

## ⚠️ Paso 5: Limpieza (Recomendado)

Una vez recuperado el acceso, es muy importante revertir los cambios por seguridad y para restaurar la funcionalidad del CMD original.

1.  Repite el **Paso 1** (Arrancar desde USB y `Shift + F10`).
2.  Usa el método del `notepad` para ir a `C:\Windows\System32`.
3.  Renombra el archivo que ahora se llama `utilman` a `cmd`.
4.  Renombra `utilman1` a `utilman`.
