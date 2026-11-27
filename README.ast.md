# Constructor de kernel personalizáu d'Ubuntu + media tree de LinuxTV.org

Esti proyeutu constrúi paquetes de kernel d'Ubuntu instalables qu'incluyen los
controladores más recientes del media tree de LinuxTV.org, con soporte estra pa dispositivos Hauppauge.

## Característiques

- Introduz el media tree más reciente de LinuxTV.org nel códigu fonte del kernel d'Ubuntu.
- Aplica los parches mínimos necesarios pa compilar.
- Xenera paquetes `.deb` instalables del kernel.
- Apurre paquetes virtuales pa una instalación y actualizaciones sencielles.
- Da soporte a un PPA pa usuarios finales.

## Requisitos

- Ubuntu (versiones soportaes: mira `patches/` (les versiones más nueves, como 26.04.1/26.10, usen el conxuntu de parches disponible más reciente)).
- Ferramientes de compilación: `git`, `make`, `patch`, `fakeroot`, `debuild`, `equivs-build`.
- Espaciu en discu y tiempu suficientes (les compilaciones del kernel son grandes).

Instalar les dependencies de compilación (exemplu):

```
sudo apt-get update
sudo apt-get install -y git make patch fakeroot devscripts equivs build-essential libncurses-dev
```

## Entamu rápidu (compilación completa)

1. Inicializar repositorios:

```
./mediatree-kbuild.sh -i
```

2. Baxar y xenerar los tarballs del media tree de LinuxTV:

```
./mediatree-kbuild.sh -m
```

3. (Opcional) Reiniciar el directoriu de compilación del kernel a un estáu llimpiu:

```
./mediatree-kbuild.sh -r
```

4. Aplicar los parches de kbuild de mediatree:

```
./mediatree-kbuild.sh -p
```

5. Aplicar parches estras:

```
./mediatree-kbuild.sh -x
```

6. Xenerar datos de compilación y llimpiar:

```
./mediatree-kbuild.sh -c
```

7. Compilar el kernel:

```
./mediatree-kbuild.sh -b
```

   O escoyer un tipu de compilación:

```
./mediatree-kbuild.sh -B full
./mediatree-kbuild.sh -B debug
```

8. Pasu final (creación de deb / controladores / kernel.org):

```
./mediatree-kbuild.sh -F
```

## PPA / paquete virtual

Xenerar descriptores del PPA:

```
./mediatree-kbuild.sh -V virtual
./mediatree-kbuild.sh -V kernel
./mediatree-kbuild.sh -V all
```

## Instalar dende'l PPA (usuarios finales)

```
sudo add-apt-repository ppa:b-rad/kernel+mediatree+hauppauge
sudo apt-get update
sudo apt-get install linux-mediatree        # all Ubuntu
# or, for LTS with HWE:
sudo apt-get install linux-hwe-mediatree
```

## Compilación completa automática (un solu comandu)

Baxa los controladores, aplícalos al kernel, compila y crea'l `.deb` nun solu pasu:

```
./mediatree-kbuild.sh -A
```

Esto executa tola tubería: inicialización, baxada del media tree, parcheo, compilación y xeneración del deb/PPA.

## Desinstalar

```
./mediatree-kbuild.sh -U k   # uninstall kernel (virtual packages)
./mediatree-kbuild.sh -U d   # remove media tree/drivers workspace
./mediatree-kbuild.sh -U p   # remove PPA
./mediatree-kbuild.sh -U a   # all of the above
```

## Otros comandos útiles

- Xenerar un conxuntu completu de parches: `./mediatree-kbuild.sh -g`
- Amosar l'ayuda: `./mediatree-kbuild.sh -h`

## Autores

- Autor del repositoriu orixinal: Brad Love <brad at nextdimension dot cc>
- Mantenedor del fork y axustes: BENDER (BENDER35)

## Llicencia

GNU General Public License v3 o posterior.


## Debian y distribuciones basaes en Debian

Soporte esperimental: el script usa como base les fontes del kernel d'Ubuntu en distribuciones basaes en Debian (Debian, Linux Mint, Pop!_OS, etc.).


## openSUSE / SUSE

Soporte esperimental: usa como base les fontes del kernel d'Ubuntu en sistemes openSUSE/SUSE.


## Distribuciones adicionales

Soporte esperimental de reserva pa: Arch Linux, Manjaro, Fedora, RHEL/CentOS/Rocky/Alma, Linux Mint, SparkyLinux, Devuan, openSUSE/SUSE. Toes usen como base les fontes del kernel d'Ubuntu.


## Paquete RPM

Xenerar un RPM de la ferramienta (rique `rpmbuild`):

```
./mediatree-kbuild.sh -R
```


## Controladores y firmware nel kernel en funcionamientu

La opción 1 de `-F` compila los módulos del media tree pa'l kernel en funcionamientu ya instala `linux-firmware` pa dispositivos Hauppauge.
