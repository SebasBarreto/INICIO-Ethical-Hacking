Tarea Semana 1 - Ethical Hacking
Introducción

Este informe detalla los pasos realizados para resolver tres ejercicios de ethical hacking. Los retos incluyen el análisis de datos filtrados, la identificación de contraseñas y servidores VPN, demostrando habilidades en el manejo de herramientas OSINT y técnicas de análisis.
Ejercicio 1: Contraseña del Administrador de Toyota

Objetivo: Encontrar la contraseña del usuario administrador Rainer Luecke en el dominio toyota.de.

    Recopilación de información inicial:
        Se utilizó la plataforma Intelligence X (phonebook.cz) para buscar correos con el dominio toyota.de.
        Resultado: Se identificaron 268 correos, con dos posibles correos asociados al nombre "Rainer":
            rainer.luecke@toyota.de
            ingeborgu.rainer.hamann@toyota.de
        Se seleccionó el primero por coincidir con nombre y apellido.

    Obtención de contraseñas filtradas:
        Descarga de un dataset de contraseñas filtradas (~41GB) desde un repositorio de GitHub.

    Búsqueda de coincidencias:
        Renombrar los archivos a .txt con PowerShell:

        Get-ChildItem -File -Recurse | ForEach-Object { Rename-Item $_.FullName -NewName "$($_.BaseName).txt" }

        Utilizar Notepad++ para buscar el dominio toyota.de y el correo identificado:
            Resultado: rainer.luecke@toyota.de:Luecke99

    Resultado:
        Correo: rainer.luecke@toyota.de
        Contraseña: Luecke99

Ejercicio 2: Contraseña del Hacker Root

Objetivo: Identificar la contraseña del correo hacker con la dirección parcial hacker-root___@live.cn.

    Recopilación inicial:
        Uso del dataset previamente descargado.

    Búsqueda de coincidencias:
        En Notepad++, se filtraron los resultados para el dominio @live.cn y la cadena hacker-root___.

    Resultado:
        Correo: hacker-rootkit@live.cn
        Contraseña: shjzcy@#

Ejercicio 3: VPN de Tesla en Japón

Objetivo: Encontrar el nombre y la dirección IP del servidor VPN instalado por Tesla en Japón.

    Identificación inicial:
        Visita al sitio oficial japonés de Tesla: tesla.com/ja_jp.
        Uso del plugin Shodan para obtener la dirección IP del servidor.

    Resolución directa e inversa de DNS:
        Comandos ejecutados en Kali Linux:

        dig tesla.com
        dig -x 104.89.224.221

        Resultado:
            Dirección IP: 104.89.224.221
            Nombre del dominio: a104-89-224-221.deploy.static.akamaitechnologies.com (VPN proporcionada por Akamai Technologies).

    Verificación con DNSDumpster:
        Se utilizó la herramienta en línea para corroborar información adicional.
        Resultado alternativo: IP 8.244.131.215 asociada a apacvpn1.tesla.com.

    Conclusión:
        Primera respuesta: 104.89.224.221 (Akamai Technologies).
        Respuesta alternativa: 8.244.131.215 (Tesla Japón).

Conclusiones

    Éxitos:
        Contraseña del administrador de Toyota: Luecke99.
        Contraseña del hacker root: shjzcy@#.
        Identificación de servidores VPN de Tesla.

    Desafíos:
        Complejidad en la búsqueda inversa de DNS para las direcciones de Tesla.
        Validación de múltiples resultados con herramientas OSINT.