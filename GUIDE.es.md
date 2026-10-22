# Guía: constructor de kernel con media tree

## ¿Qué es un kernel?

El kernel es el núcleo del sistema operativo. Gestiona el hardware, los procesos,
la memoria y los drivers. En Linux, los drivers de dispositivos (sintonizadores
de TV, tarjetas de captura) viven dentro del árbol de código fuente del kernel.

## ¿Qué son los drivers de Hauppauge?

Los sintonizadores y dispositivos de captura Hauppauge usan drivers del subsistema
media del kernel (V4L2/DVB). El media tree de LinuxTV.org contiene las versiones
más recientes de estos drivers, incluyendo correcciones y nuevos IDs de dispositivo
que puede que aún no estén en el kernel de Ubuntu.

## Cómo funciona este script

`mediatree-kbuild.sh` automatiza:

1. Descarga del código fuente del kernel de Ubuntu para una versión.
2. Descarga del media tree de LinuxTV.
3. Generación de un tarball del media tree parcheado para la versión del kernel.
4. Aplicación de parches al código fuente del kernel de Ubuntu.
5. Actualización de metadatos y changelog de compilación.
6. Compilación de paquetes `.deb` instalables.

## Flujo de trabajo

- `-i`: inicializar/actualizar repositorios git.
- `-m`: descargar y generar tarballs del media tree.
- `-r`: resetear a estado limpio el directorio de compilación.
- `-p`: aplicar parches mediatree.
- `-x`: aplicar parches adicionales.
- `-c`: regenerar datos de compilación y limpiar.
- `-b` / `-B`: compilar el kernel.
- `-F`: menú final (aplicar drivers, crear deb, descargar kernel.org, aplicar al kernel en ejecución).
- `-U`: desinstalar kernel/drivers/PPA.

## Compilación

La compilación del kernel usa `debian/rules` con `fakeroot`. Produce paquetes
`.deb` de imagen, módulos, cabeceras y módulos extra.

## Diferencias con Windows

- En Windows, los drivers suelen instalarse como paquetes separados del fabricante.
- En Linux, los drivers de media forman parte del árbol de código fuente del kernel
  y se compilan con el kernel (o como módulos fuera del árbol).
- Actualizar drivers en Linux suele implicar actualizar el kernel (o recompilar módulos).
- Este proyecto entrega los drivers mediante paquetes `.deb` estándar de Ubuntu y un PPA,
  por lo que las actualizaciones llegan vía `apt`.

## Desinstalación

Usa `-U` para eliminar los paquetes virtuales del kernel instalado, el espacio
de trabajo del media tree o el PPA.


## Construcción automática completa (un solo comando)

Descarga los drivers, los añade al kernel, compila y crea el `.deb` en un solo paso:

```
./mediatree-kbuild.sh -A
```

Esto ejecuta toda la tubería: inicialización, descarga del media tree, parcheo, compilación y generación del deb/PPA.


## Debian y distribuciones basadas en Debian

Soporte experimental: el script usa como base las fuentes del kernel de Ubuntu en distros basadas en Debian (Debian, Linux Mint, Pop!_OS, etc.).


## openSUSE / SUSE

Soporte experimental: usa como base las fuentes del kernel de Ubuntu en sistemas openSUSE/SUSE.


## Distribuciones adicionales

Soporte experimental de fallback para: Arch Linux, Manjaro, Fedora, RHEL/CentOS/Rocky/Alma, Linux Mint, SparkyLinux, Devuan, openSUSE/SUSE. Todas usan como base las fuentes del kernel de Ubuntu.
