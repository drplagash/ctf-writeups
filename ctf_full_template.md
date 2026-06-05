# CTF / Writeup Template

> Uso: copiá este archivo dentro de la carpeta de cada máquina o laboratorio y completalo.
>
> Alcance: laboratorios autorizados, CTFs, DockerLabs, PortSwigger, VulnHub, TryHackMe, Hack The Box o entornos propios.
>
> No publicar credenciales reales, tokens, dumps, datos sensibles ni targets de terceros.

---

## 1. Información general

```text
Nombre:
Plataforma:
Categoría:
Dificultad:
Sistema operativo:
Fecha:
Autor:
Estado:
```

## 2. Alcance

```text
Entorno autorizado:
IP objetivo:
Dominio/host:
Red:
Notas de alcance:
```

Ejemplo:

```text
Entorno autorizado: DockerLabs local
IP objetivo: 172.17.0.2
Red: docker bridge local
Notas de alcance: práctica local, sin terceros
```

---

## 3. Preparación del workspace

Estructura sugerida:

```text
machine-name/
├── README.md
├── nmap/
├── web/
├── fuzzing/
├── exploit/
├── payloads/
├── privesc/
├── loot-redacted/
├── screenshots/
└── notes.md
```

Comandos base:

```bash
mkdir -p nmap web fuzzing exploit payloads privesc loot-redacted screenshots
```

---

## 4. Enumeración inicial

### 4.1 Ping / conectividad

```bash
ping -c 4 <TARGET_IP>
```

Resultado:

```text
[pegar resultado relevante]
```

Notas:

```text
TTL:
Hipótesis de sistema operativo:
Latencia:
```

---

## 5. Nmap

### 5.1 Escaneo rápido de puertos

```bash
nmap -p- --open --min-rate 5000 -n -Pn <TARGET_IP> -oN nmap/all_ports.txt
```

Resultado:

```text
[pegar puertos abiertos]
```

### 5.2 Escaneo de servicios y scripts básicos

```bash
nmap -sC -sV -p <PORTS> <TARGET_IP> -oN nmap/services.txt
```

Resultado:

```text
[pegar versiones detectadas]
```

### 5.3 Escaneo UDP opcional

```bash
sudo nmap -sU --top-ports 100 <TARGET_IP> -oN nmap/udp_top100.txt
```

Resultado:

```text
[pegar hallazgos si aplica]
```

### 5.4 Resumen de puertos

| Puerto | Servicio | Versión | Observación | Prioridad |
|---|---|---|---|---|
|  |  |  |  |  |

---

## 6. Enumeración web

> Completar solo si hay HTTP/HTTPS u otro servicio web.

### 6.1 Identificación básica

```bash
curl -i http://<TARGET_IP>/
```

```bash
whatweb http://<TARGET_IP>/
```

Resultado:

```text
[headers, tecnologías, servidor, cookies]
```

### 6.2 Navegación manual

```text
URL:
Título:
Tecnologías:
Login:
Formularios:
Comentarios HTML:
Rutas interesantes:
```

### 6.3 Capturas

```text
screenshots/home.png
screenshots/login.png
screenshots/error.png
```

---

## 7. Fuzzing web

### 7.1 Gobuster

```bash
gobuster dir -u http://<TARGET_IP>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -x php,txt,html,bak -o fuzzing/gobuster_common.txt
```

Resultado:

```text
[pegar rutas útiles]
```

### 7.2 FFUF

```bash
ffuf -u http://<TARGET_IP>/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc all -o fuzzing/ffuf_common.md -of md
```

Si hay muchos falsos positivos por tamaño:

```bash
ffuf -u http://<TARGET_IP>/FUZZ -w /usr/share/seclists/Discovery/Web-Content/common.txt -fs <SIZE> -mc all -o fuzzing/ffuf_filtered.md -of md
```

Resultado:

```text
[pegar rutas útiles]
```

### 7.3 Parámetros

```bash
ffuf -u "http://<TARGET_IP>/<PATH>?FUZZ=test" -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -mc all -o fuzzing/params.md -of md
```

Resultado:

```text
[parámetros interesantes]
```

---

## 8. Enumeración por servicio

### 8.1 FTP

```bash
nmap --script ftp-anon,ftp-syst -p 21 <TARGET_IP> -oN nmap/ftp_scripts.txt
```

Notas:

```text
Anonymous login:
Archivos:
Permisos:
Hallazgos:
```

### 8.2 SSH

```text
Puerto:
Versión:
Usuarios posibles:
Método de acceso:
```

> No publicar credenciales reales. En CTF, redactar si hace falta.

### 8.3 SMB

```bash
smbclient -L //<TARGET_IP>/ -N
```

```bash
enum4linux-ng <TARGET_IP> -oA nmap/enum4linux
```

Notas:

```text
Shares:
Usuarios:
Permisos:
Hallazgos:
```

### 8.4 DNS

```bash
dig @<TARGET_IP> <DOMAIN>
```

```bash
dig axfr @<TARGET_IP> <DOMAIN>
```

Notas:

```text
Dominio:
Registros:
Zone transfer:
Subdominios:
```

### 8.5 Otros servicios

```text
Servicio:
Puerto:
Versión:
Herramientas usadas:
Hallazgos:
```

---

## 9. Análisis de vulnerabilidades

### 9.1 Hallazgos candidatos

```text
Hallazgo 1:
Servicio:
Evidencia:
Impacto posible:
Fuente/referencia:
Prioridad:
```

### 9.2 Búsqueda de exploits públicos

```bash
searchsploit <PRODUCT> <VERSION>
```

Resultado:

```text
[pegar solo referencias útiles, no basura]
```

### 9.3 Validación manual

```text
Vulnerabilidad:
Condición necesaria:
Se cumple en el lab:
Evidencia:
Riesgo:
```

---

## 10. Explotación

> Solo entorno autorizado. Documentar qué se hizo y por qué. Nada de targets externos.

### 10.1 Vector elegido

```text
Vector:
Servicio:
Motivo:
Evidencia previa:
```

### 10.2 Comandos usados

```bash
# comandos usados en el lab
```

### 10.3 Resultado

```text
Resultado:
Usuario obtenido:
Acceso:
Limitaciones:
```

### 10.4 Evidencia

```text
screenshots/exploit_result.png
exploit/output.txt
```

---

## 11. Payloads observados o usados

### 11.1 Payload bruto

> Sanitizar si contiene secretos, tokens, flags o datos sensibles.

```text
[PAYLOAD SANITIZADO]
```

### 11.2 Decodificación

```text
Formato:
Encoding:
Transformaciones:
Herramientas:
```

Ejemplos útiles:

```bash
echo '<BASE64>' | base64 -d
```

```bash
python3 - <<'PY'
from urllib.parse import unquote
print(unquote("<URL_ENCODED_STRING>"))
PY
```

### 11.3 Interpretación

```text
Objetivo del payload:
Técnica:
Servicio afectado:
Indicadores:
Riesgo:
```

### 11.4 Detección defensiva

```text
Logs:
Patrones:
YARA/Sigma/Suricata:
Comportamiento:
```

---

## 12. Post-explotación básica

### 12.1 Identidad

```bash
whoami
id
hostname
```

Resultado:

```text
[pegar salida]
```

### 12.2 Sistema

```bash
uname -a
cat /etc/os-release
```

Resultado:

```text
[pegar salida]
```

### 12.3 Red

```bash
ip a
ip route
ss -tulpn
```

Resultado:

```text
[pegar salida]
```

---

## 13. Escalada de privilegios

### 13.1 Enumeración manual Linux

```bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
find / -writable -type d 2>/dev/null
cat /etc/passwd
```

Notas:

```text
Sudo:
SUID:
Capabilities:
Cron:
Procesos:
Archivos escribibles:
Credenciales encontradas:
```

### 13.2 Herramientas opcionales

```bash
# LinPEAS, Linux Smart Enumeration u otra herramienta solo si el lab lo permite
```

Resultado:

```text
[resumen, no pegar 10.000 líneas salvo que haga falta]
```

### 13.3 Vector de escalada

```text
Vector:
Evidencia:
Comando:
Resultado:
Usuario final:
```

---

## 14. Flags / evidencia sensible

> Redactar si se publica públicamente.

```text
user.txt: [REDACTED]
root.txt: [REDACTED]
```

---

## 15. Limpieza

```text
Archivos creados:
Procesos iniciados:
Cambios realizados:
Limpieza realizada:
```

Comandos:

```bash
# comandos de limpieza si aplica
```

---

## 16. Notas defensivas

```text
Qué falló:
Cómo detectarlo:
Cómo mitigarlo:
Qué logs mirar:
Qué controles aplicar:
```

Ejemplo:

```text
Control:
- Deshabilitar credenciales débiles.
- Restringir permisos.
- Actualizar versión vulnerable.
- Monitorear rutas accedidas.
- Alertar por patrones de payload.
```

---

## 17. Lecciones aprendidas

```text
1.
2.
3.
```

---

## 18. Referencias

```text
- NVD:
- Vendor:
- Exploit-DB:
- GTFOBins:
- HackTricks:
- PayloadsAllTheThings:
- Documentación oficial:
```

---

## 19. Resumen ejecutivo

```text
La máquina/lab expuso [servicio/vulnerabilidad].
El acceso inicial se logró mediante [vector].
La escalada se logró mediante [vector].
El impacto principal fue [impacto].
La mitigación recomendada es [acción].
```

---

## 20. Estado final

```text
Acceso inicial:
Escalada:
Writeup completo:
Capturas:
Código:
Pendiente:
```

---

## Disclaimer

Este documento es para aprendizaje, investigación defensiva y laboratorios autorizados.  
No usar contra sistemas de terceros.  
No publicar secretos, credenciales, dumps, tokens ni datos sensibles.

**Menos humo, más evidencia.**
