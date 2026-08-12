+++
title = 'Plantilla PPI'
weight = 5
+++

Herramienta de trabajo (ámbito sociosanitario): `extract_dietas.py` extrae datos de
PDFs de planificación de dietas/menús y genera un PDF de una sola cara listo para
imprimir (`pdfplumber` para leer, `reportlab` para maquetar en A4 apaisado con tablas).
`dietas_consolidado.json`/`.pdf` son la salida consolidada; `PLANTILLA PPI
CORREGIDA.docx` y `ASISTIDOS.pdf` son las plantillas/documentos de partida del proceso
que automatiza.
