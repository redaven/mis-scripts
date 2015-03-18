Diferentes scripts que voy creando para solucionarme la papeleta.

# Cloner #

Es una utilidad que hace poco que he creado me sirve para tener imagenes de las maquinas
que clono con udpcast.

udpcast tiene un pequeño problema si no usas imágenes es que si en esa maquina ya han trabajado te puedes encontrar que a la próxima restauración de una maquina que funcione este llena de mierda _( Archivos de los usuarios , alguna que otro virus etc)_

La instalación es muy fácil tienes de instalar udpcast esta en los repos de debian.
luego descargas el cloner y lo instalas así.
```
# wget http://mis-scripts.googlecode.com/files/cloner.tar.gz
# tar xvf cloner.tar.gz -C /
# ln -s /usr/bin/restaurar /bin/restaurar
```

Ahora puedes clonar de forma normal con udpcast.

[WikiDeHouseOfSysAdmins](http://wiki.houseofsysadmins.com/spip.php?article15)

Aquí encontrareis el procedimiento a seguir.

En la maquina de las imagenes tras configurar _/etc/cloner.conf_ definiendo la partición donde nos guardara las imágenes tipo de compresión etc.

**Nota:** _La compresión tiene que ser igual en los clientes como en el script_

ejecutamos en la maquina de las imágenes.

creaimagen nombreimagen.img

Esto creara la imagen en la partición que le hemos indicado.

Luego para restaurar las maquinas simplemente tenemos de ejecutar

_# restaurar_

esto nos mostrara la lista de maquinas así

```
1) aaa 
2) PC-01 
3) PC-10 
4) PC-1 
5) PC-2 
6) PC-3 
7) PC-4 
8) PC-5 
9) PC-6 
10) PC-7 
11) PC-8 
12) PC-9 
0) Salir

Haga su Seleccion [0-12]: 


```

Seleccionamos la imagen y pasara a clonarse a los clientes.

# LTSP Desatendido Linkat o Suse Linux Enterprise Desktop 10 #

[MirarEnLawiki](http://code.google.com/p/mis-scripts/wiki/LTSPLinkatOSuseLinuxEnterpriseDesktop)

# Llug Optimizer #

Es un pequeño script que optimiza una ubuntu fácilmente
_Code:_

```
#!/bin/bash
## Llug Ubuntu Optimize.

### Creat el 17/4/09

## 1. Upstart arranc Paralel

sed -r -i s/CONCURRENCY=.+/CONCURRENCY=shell/g /etc/init.d/rc

### 2. Activació noatime a les particions.
sed -r -i s/relatime,.+/”noatime,errors=remount-ro 0 1″/g /etc/fstab

### 3. Accelerar Menus gnome a tots els usuaris

for users in $(ls /home/) ;do echo ‘echo “gtk-menu-popup-delay = 0″ >>’ /home/$users/.gtkrc-2.0 ;done |bash -

### 4. Eliminar Terminals virtuals.

mv /etc/event.d/tty3 /etc/event.d/tty3.bkp
mv /etc/event.d/tty4 /etc/event.d/tty4.bkp

### 5. Instaŀlar Preload
apt-get update
apt-get install preload

### 6. Reduir espai Intercambi Swap
echo “vm.swappiness = 10″ >> /etc/sysctl.conf

### 7. Deshabilitar ipv6

sed -r -i s/”alias net-pf-10 ipv6″/”alias net-pf-10 off #ipv6″/g /etc/modprobe.d/aliases
```

El script hace lo siguiente:
  * Arranque en paralelo
  * Activa noatime en las particiones
  * Acelera los menús de gnome para todos los usuarios
  * Elimina las terminales virtuales 3 y 4
  * Instala Preload _(Precarga de las aplicaciones mas usadas)_
  * Reduce el espacio usado por la swap
  * Deshabilita el ipv6

Puedes optimizar tu ubuntu de la siguiente forma

_$ sudo su_

_# wget -q  http://mis-scripts.googlecode.com/files/LLugOptimitza.sh   -O- |bash -_