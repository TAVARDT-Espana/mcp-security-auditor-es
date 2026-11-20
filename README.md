# Auditor de Seguridad para Servidores y Herramientas MCP

[![Live Demo](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-06b6d4?style=for-the-badge)](https://tavardt-espana.github.io/mcp-security-auditor-es/)
[![Standard](https://img.shields.io/badge/Standard-EU%20Cybersecurity-3b82f6?style=for-the-badge)](https://tavardt-espana.github.io/mcp-security-auditor-es/)
[![Privacy](https://img.shields.io/badge/Privacy-100%25%20Client--Side-10b981?style=for-the-badge)](https://tavardt-espana.github.io/mcp-security-auditor-es/)
[![License](https://img.shields.io/badge/License-MIT-slate?style=for-the-badge)](LICENSE)

Auditor de seguridad para servidores y herramientas MCP (Model Context Protocol). Aplicacion web en cliente y CLI.

Desarrollado para organizaciones y profesionales en **Espana**, este repositorio ofrece una solucion tecnica integral para auditar y robustecer configuraciones del **Model Context Protocol (MCP)** en entornos de inteligencia artificial.

---

## Modos de Operacion

### 1. Aplicacion Web en Navegador (GitHub Pages)
Acceda a la aplicacion interactiva sin instalar software:
- **Enlace Oficial**: [https://tavardt-espana.github.io/mcp-security-auditor-es/](https://tavardt-espana.github.io/mcp-security-auditor-es/)
- **Privacidad Total**: Procesamiento realizado integramente en el motor JavaScript de su navegador. Ningun dato o clave se envia a servidores externos.

### 2. Herramienta de Linea de Comandos (CLI)
Para ejecucion automatizada en tuberias de integracion continua (CI/CD) o auditorias locales:

```bash
# Analisis basico indicando la ruta del fichero de configuracion
python mcp_security_scanner.py --file mcp.json

# Modo estricto para despliegues seguros (retorna codigo 1 ante cualquier hallazgo)
python mcp_security_scanner.py --file mcp.json --strict

# Generacion automatica de configuracion blindada (Hardened)
python mcp_security_scanner.py --file mcp.json --harden mcp-hardened.json

# Salida estructurada en JSON
python mcp_security_scanner.py --file mcp.json --json
```

---

## Vectores de Seguridad Evaluados

1. **Alcance en Sistema de Ficheros**: Deteccion de montajes en directorios raiz (`/`, `C:\`) o rutas criticas del sistema (`/etc`, `~/.ssh`).
2. **Ejecucion Arbitraria de Comandos**: Bloqueo de interpretes directos de terminal (`bash`, `sh`, `powershell`, `cmd`) y parametros dinamicos riesgosos.
3. **Exposicion de Secretos y Credenciales**: Localizacion de contrasenas, tokens privados y cadenas de conexion en texto plano.
4. **Seguridad en Cadena de Suministro**: Verificacion de fijacion estricta de versiones en paquetes remotos (`npx`, `uvx`).
5. **Prevencion de SSRF y Metadatos**: Control de peticiones dirigidas a interfaces locales o direcciones de metadatos en la nube (`169.254.169.254`).

---

## Ejemplo de Integracion en GitHub Actions

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
      - name: Ejecutar Auditoria MCP
        run: |
          python mcp_security_scanner.py --file config/mcp.json --strict
```

---

## Estandares Institucionales y Conformidad

- **Jurisdiccion**: Espana
- **Marco Tecnico**: Estandares Europeos de Seguridad en IA y Arquitectura de Menor Privilegio
- **Organizacion Responsable**: [TAVARDT-Espana](https://github.com/TAVARDT-Espana)

## Ecosistema y Enlaces TAVARDT

- **Portal Institucional**: [https://ag.tavardt.com/es/](https://ag.tavardt.com/es/)
- **Herramientas de Ciberseguridad**: [https://tools.tavardt.com/es/](https://tools.tavardt.com/es/)
- **Canal de Contacto Tecnico**: [https://ag.tavardt.com/es/contacto/](https://ag.tavardt.com/es/contacto/)

---

### Licencia
Distribuido bajo licencia MIT. Consulte el archivo [LICENSE](LICENSE) para mas detalles.
