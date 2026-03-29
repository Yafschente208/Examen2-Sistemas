# Examen 2 - CI/CD con GitHub Actions y Docker

##  Descripción
Proyecto del examen de Sistemas Operativos I donde se implementa:
- Dockerfile
- Docker Compose
- Pipeline CI
- Pipeline CD

---

##  Docker

### Dockerfile
Se creó un Dockerfile para ejecutar una aplicación Node.js.

### Docker Compose
Se configuró docker-compose.yml con:
- Servicio web (Node.js)
- Servicio base de datos (MongoDB)
- Volumen persistente
- Red personalizada

---

##  CI (Continuous Integration)

Se creó un workflow en:
.github/workflows/ci.yml

Este pipeline ejecuta:
- lint
- test
- coverage

Se usa:
- matrix con Node 18 y 20
- cache de npm

---

##  CD (Continuous Deployment)

Se creó un workflow en:
.github/workflows/cd.yml

Este pipeline:
- Se ejecuta en push a main
- Usa environment: production
- Usa secrets (DEPLOY_KEY, API_TOKEN)
- Simula un deploy exitoso

---

## Actividad 4: Troubleshooting

### Snippet 1
Error: falta el `:` en los trigger.

Corrección:
```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main, develop]
```

### Snippet 2
Error: uso incorrecto de secrets.

Corrección:
```yaml
env:
  VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```

### Snippet 3
Error: matrix mal definida y cache mal ubicado.

Corrección:
```yaml
strategy:
  matrix:
    node-version: [18, 20]

- uses: actions/setup-node@v4
  with:
    node-version: ${{ matrix.node-version }}
    cache: npm
```