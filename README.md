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
## Evidencia
Pipelines CI y CD ejecutados correctamente en GitHub Actions.
```
```
## Actividad 5: Conceptos

### 1. Diferencia entre CI y CD
CI básicamente es cuando el sistema prueba el código automáticamente cada vez que uno hace cambios, para ver que no esté todo roto.  
CD ya es cuando después de que todo pasa bien, el sistema se encarga de desplegar o “subir” la aplicación automáticamente.

### 2. Self-hosted runner
Es como usar tu propia computadora o servidor para ejecutar los workflows en lugar de usar los de GitHub.  
Sirve cuando ocupás más control o cosas específicas que GitHub no tiene.

### 3. GitHub environments
Son como ambientes, por ejemplo production o development, donde podés manejar cosas como secretos o configuraciones diferentes para cada uno.

### 4. Rollback strategy
Es básicamente tener una forma de volver atrás a una versión anterior si algo sale mal después de un deploy.