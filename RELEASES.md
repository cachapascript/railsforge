# Flujo de Releases - RailsForge

## Flujo Ideal para Releases

### 1. Desarrollo en Feature Branches

```bash
# Crear una rama para la nueva funcionalidad
git checkout -b feature/nombre-de-la-feature

# Hacer los cambios
# ...

# Commit siguiendo convenciones (Conventional Commits)
git commit -m "feat: descripción de la funcionalidad"

# Push de la rama
git push origin feature/nombre-de-la-feature
```

### 2. Pull Request (PR)

1. Ir a GitHub y crear un Pull Request desde la feature branch hacia `main`
2. Revisar el código (self-review o peer review)
3. Asegurarse de que los checks pasen (si hay CI/CD)
4. Mergear el PR a `main`

### 3. Crear Tag (Versionado Semántico)

```bash
# Actualizar main
git checkout main
git pull origin main

# Crear tag semántico
# MAJOR.MINOR.PATCH
# - MAJOR: Cambios incompatibles
# - MINOR: Nuevas funcionalidades compatibles
# - PATCH: Bug fixes
git tag -a v1.1.0 -m "feat: Add custom README generation with project name"

# Subir el tag
git push origin v1.1.0
```

### 4. Crear GitHub Release

1. Ir a GitHub → Releases → "Draft a new release"
2. Seleccionar el tag creado
3. Escribir notas de release:
   - Nuevas funcionalidades
   - Bug fixes
   - Breaking changes
   - Mejoras
4. Publicar el release

### 5. Ejemplo Completo

```bash
# 1. Crear feature branch
git checkout -b feature/custom-readme

# 2. Hacer cambios y commits
git add .
git commit -m "feat: Generate custom README with project name"

# 3. Push y crear PR
git push origin feature/custom-readme

# 4. Mergear PR en GitHub

# 5. Actualizar main y crear tag
git checkout main
git pull origin main
git tag -a v1.1.0 -m "Add custom README generation"
git push origin v1.1.0

# 6. Crear Release en GitHub
```

## Convenciones de Commits

- `feat:` Nueva funcionalidad
- `fix:` Corrección de bug
- `docs:` Cambios en documentación
- `refactor:` Refactorización de código
- `test:` Cambios en tests
- `chore:` Tareas de mantenimiento

## Versionado Semántico

- **v1.0.0** → Primera versión estable
- **v1.1.0** → Nueva funcionalidad (minor)
- **v1.1.1** → Bug fix (patch)
- **v2.0.0** → Cambio incompatible (major)

## Checklist antes de Release

- [ ] Todos los PRs mergeados a main
- [ ] Tests pasando (si aplica)
- [ ] Documentación actualizada
- [ ] Changelog actualizado
- [ ] Tag creado con versionado semántico
- [ ] Release creado en GitHub con notas
