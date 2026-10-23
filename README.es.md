# Constructor de kernel personalizado Ubuntu + LinuxTV.org media tree

Este proyecto construye paquetes de kernel de Ubuntu instalables que incluyen
los últimos drivers del media tree de LinuxTV.org, con soporte adicional para
dispositivos Hauppauge.

## Características

- Inserta el media tree más reciente de LinuxTV.org en el código fuente del kernel de Ubuntu.
- Aplica los parches mínimos necesarios para compilar.
- Genera paquetes `.deb` instalables del kernel.
- Proporciona paquetes virtuales para instalación y actualización sencillas.
- Soporta un PPA para usuarios finales.

## Requisitos

- Ubuntu (versiones soportadas: ver `patches/`).
- Herramientas de compilación: `git`, `make`, `patch`, `fakeroot`, `debuild`, `equivs-build`.
- Espacio en disco suficiente y tiempo (la compilación del kernel es grande).

Instalar dependencias (ejemplo):

```
sudo apt-get update
sudo apt-get install -y git make patch fakeroot devscripts equivs build-essential libncurses-dev
```

## Inicio rápido (compilación completa)

1. Inicializar repositorios:

```
./mediatree-kbuild.sh -i
```

2. Descargar y generar los tarballs del media tree de LinuxTV:

```
./mediatree-kbuild.sh -m
```

3. (Opcional) Resetear el directorio de compilación a estado limpio:

```
./mediatree-kbuild.sh -r
```

4. Aplicar los parches del sistema de compilación mediatree:

```
./mediatree-kbuild.sh -p
```

5. Aplicar parches adicionales:

```
./mediatree-kbuild.sh -x
```

6. Generar datos de compilación y limpiar:

```
./mediatree-kbuild.sh -c
```

7. Compilar el kernel:

```
./mediatree-kbuild.sh -b
```

   O elegir tipo de compilación:

```
./mediatree-kbuild.sh -B full
./mediatree-kbuild.sh -B debug
```

8. Paso final (creación de deb / drivers / kernel.org):

```
./mediatree-kbuild.sh -F
```

## PPA / paquete virtual

Construir descriptores del PPA:

```
./mediatree-kbuild.sh -V virtual
./mediatree-kbuild.sh -V kernel
./mediatree-kbuild.sh -V all
```

## Instalar desde el PPA (usuarios finales)

```
sudo add-apt-repository ppa:b-rad/kernel+mediatree+hauppauge
sudo apt-get update
sudo apt-get install linux-mediatree        # todos los Ubuntu
# o, para LTS con HWE:
sudo apt-get install linux-hwe-mediatree
```

## Construcción automática completa (un solo comando)

Descarga los drivers, los añade al kernel, compila y crea el `.deb` en un solo paso:

```
./mediatree-kbuild.sh -A
```

Esto ejecuta toda la tubería: inicialización, descarga del media tree, parcheo, compilación y generación del deb/PPA.

## Desinstalar

```
./mediatree-kbuild.sh -U k   # desinstalar kernel (paquetes virtuales)
./mediatree-kbuild.sh -U d   # eliminar media tree/drivers del espacio de trabajo
./mediatree-kbuild.sh -U p   # eliminar PPA
./mediatree-kbuild.sh -U a   # todo lo anterior
```

## Otros comandos útiles

- Generar conjunto completo de parches: `./mediatree-kbuild.sh -g`
- Mostrar ayuda: `./mediatree-kbuild.sh -h`

## Autores

- Autor del repositorio original: Brad Love <brad at nextdimension dot cc>
- Mantenedor del fork y ajustes: BENDER (BENDER35)

## Licencia

GNU General Public License v3 o posterior.


## Debian y distribuciones basadas en Debian

Soporte experimental: el script usa como base las fuentes del kernel de Ubuntu en distros basadas en Debian (Debian, Linux Mint, Pop!_OS, etc.).


## openSUSE / SUSE

Soporte experimental: usa como base las fuentes del kernel de Ubuntu en sistemas openSUSE/SUSE.


## Distribuciones adicionales

Soporte experimental de fallback para: Arch Linux, Manjaro, Fedora, RHEL/CentOS/Rocky/Alma, Linux Mint, SparkyLinux, Devuan, openSUSE/SUSE. Todas usan como base las fuentes del kernel de Ubuntu.


## Paquete RPM

Generar un RPM de la herramienta (requiere `rpmbuild`):

```
./mediatree-kbuild.sh -R
```


## Drivers y firmware en el kernel en ejecución

La opción 1 de `-F` compila los módulos del media tree para el kernel en ejecución e instala `linux-firmware` para dispositivos Hauppauge.
