# Docker
---

Esta es la parte más larga en tiempo de todo el trabajo, aquí explico como he hecho paso a paso un contenedor docker de NGINX para que saque la página web de este proyecto.

---

### -1 Github
Para empezar si quiero que este contendor saque mi pagina web debo cambiarme de rama a la que genera MKDocs **gh-pages** (`git checkout -b gh-pages`), desde aquí tengo que clonar los datos a la máquina kali (`git pull`).

![git pull](https://raw.githubusercontent.com/vjp-hectorBG/PPS-Unidad0-Tarea-Hector_Blazquez_Gomez/refs/heads/main/imgs/pull.png)

### -2 Kali

Luego deberemos hacer un volumen **Bind Mount** sobre el contenedor para que este acceda a los documentos en ese momento, tambien he cambiado el puerto al 8085 y el nombre al descrito abajo.

Como se puede observar en el comando he utilizado `pwd` para que pille la ruta absoluta en la que estoy actualmente , así docker tiene menos posibilidades de confundirse.

`docker run -d -p 8085:80 --name PPSUnidad0-Tarea_Hector_Blazquez_Gomez -v "$(pwd)":/usr/share/nginx/html nginx:latest`

![bind mount](https://raw.githubusercontent.com/vjp-hectorBG/PPS-Unidad0-Tarea-Hector_Blazquez_Gomez/refs/heads/main/imgs/bindmount.png)

Una vez acceda desde el puerto 8085 podremos ver la página web de mi proyecto , o en el estado en el que estaba cuando la cloné del repositorio (`http://localhost:8085/`).

![working](https://github.com/vjp-hectorBG/PPS-Unidad0-Tarea-Hector_Blazquez_Gomez/blob/main/imgs/working.png)
