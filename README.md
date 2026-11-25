# Auditor de Seguridad para Servidores y Herramientas MCP

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-5b3cf5.svg)](https://tavardt-espana.github.io/mcp-security-auditor-es/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Auditor de seguridad para servidores y herramientas MCP (Model Context Protocol). Aplicación web en cliente y CLI.

Desarrollado para organizaciones y profesionales en **España**, este repositorio ofrece una solución técnica integral para auditar y robustecer configuraciones del **Model Context Protocol (MCP)** en entornos de inteligencia artificial.

***

## Modos de Operación

### 1. Aplicación Web en Navegador (GitHub Pages)
Acceda a la aplicación interactiva sin instalar software:
- **Enlace Oficial**: [https://tavardt-espana.github.io/mcp-security-auditor-es/](https://tavardt-espana.github.io/mcp-security-auditor-es/)
- **Privacidad Total**: Procesamiento realizado íntegramente en el motor JavaScript de su navegador. Ningún dato o clave se envía a servidores externos.

### 2. Herramienta de Línea de Comandos (CLI)
Para ejecución automatizada en tuberías de integración continua (CI/CD) o auditorías locales:

```bash
# Análisis básico indicando la ruta del fichero de configuración
python mcp_security_scanner.py -file mcp.json

# Modo estricto para despliegues seguros (retorna código 1 ante cualquier hallazgo)
python mcp_security_scanner.py -file mcp.json -strict

# Generación automática de configuración blindada (Hardened)
python mcp_security_scanner.py -file mcp.json -harden mcp-hardened.json

# Salida estructurada en JSON
python mcp_security_scanner.py -file mcp.json -json
```

***

## Vectores de Seguridad Evaluados

1. **Alcance en Sistema de Ficheros**: Detección de montajes en directorios raíz (`/`, `C:\`) o rutas críticas del sistema (`/etc`, `~/.ssh`).
2. **Ejecución Arbitraria de Comandos**: Bloqueo de intérpretes directos de terminal (`bash`, `sh`, `powershell`, `cmd`) y parámetros dinámicos riesgosos.
3. **Exposición de Secretos y Credenciales**: Localización de contraseñas, tokens privados y cadenas de conexión en texto plano.
4. **Seguridad en Cadena de Suministro**: Verificación de fijación estricta de versiones en paquetes remotos (`npx`, `uvx`).
5. **Prevención de SSRF**: Control de peticiones dirigidas a interfaces locales o servicios internos no autorizados.

***

## Ejemplo de Integración en GitHub Actions

```yaml
name: MCP Security Gate
on: [push, pull_request]

jobs:
  audit-mcp:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Instalar Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Ejecutar Auditoría MCP
        run: |
          python mcp_security_scanner.py -file config/mcp.json -strict
```

***

## Estándares Institucionales y Conformidad

- **Marco Técnico**: Estándares Europeos de Seguridad en IA y Arquitectura de Menor Privilegio

## Ecosistema y Enlaces TAVARDT

- **Portal Institucional**: [Portal Institucional](https://ag.tavardt.com/es/)
- **Centro de Herramientas**: [Central de Herramientas](https://tools.tavardt.com/es/)
- **Canal de Contacto Técnico**: [https://ag.tavardt.com/es/contacto/](https://ag.tavardt.com/es/contacto/)

***

## Enlaces Útiles

* **Portal Corporativo:** https://ag.tavardt.com/es/
* **Suite de Diagnósticos:** https://tools.tavardt.com/es/
* **Contacto Técnico:** https://ag.tavardt.com/es/contacto/

***

### Licencia
Distribuido bajo licencia MIT.

***

© 2026 TAVARDT. Todos los derechos reservados.
