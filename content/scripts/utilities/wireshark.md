+++
title = 'Wireshark'
weight = 11
+++

Ruta: `~/Scripts/utilities/wireshark/`

Análisis de capturas de red (`.pcap`), con `tshark`/`scapy`, orientado a detectar
anomalías o tráfico sospechoso en la LAN propia.

| Script | Qué hace |
|---|---|
| `tcpdump_captures.sh` | Lanza la captura de tráfico con `tcpdump`. |
| `analizar_captura.sh` / `tshark_common.sh` | Extraen con `tshark` avisos de DNS (respuestas con código de error) y otros patrones comunes de la captura. |
| `analizar_http.py` / `analizar_http_404.py` | Analizan (con `scapy`) el tráfico HTTP de la captura: el segundo se centra en respuestas 404. |
| `analizar_http_files2.py` / `analizar_http_files_pw.py` | Extraen archivos transferidos por HTTP de la captura; la variante `_pw` busca específicamente contraseñas/credenciales en claro. |
| `analizar_http_fuerza_bruta.py` | Detecta patrones de fuerza bruta (muchos intentos de login) en el tráfico HTTP capturado. |
| `analizar_http_iny_codigo.py` | Busca patrones de inyección de código en peticiones HTTP capturadas. |
