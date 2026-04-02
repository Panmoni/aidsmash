# AidSmash 🚀

**Plataforma descentralizada de fundraising para non-profits basada en milestones, construida en Solana**

AidSmash conecta organizaciones sin fines de lucro directamente con donantes usando blockchain, garantizando transparencia y accountability mediante un sistema de funding basado en hitos verificables.

---

## 📋 Tabla de Contenidos

- [Acerca del Proyecto](#acerca-del-proyecto)
- [Características del MVP](#características-del-mvp)
- [Stack Tecnológico](#stack-tecnológico)
- [Inicio Rápido con Docker](#inicio-rápido-con-docker)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Desarrollo](#desarrollo)
- [Testing](#testing)
- [Documentación](#documentación)
- [Contribuir](#contribuir)

---

## 🎯 Acerca del Proyecto

AidSmash es un proyecto de ejemplo que demuestra cómo construir una aplicación descentralizada completa en Solana. El MVP incluye:

- ✅ Smart contracts en Rust usando Anchor Framework
- ✅ Frontend en React + TypeScript + Vite
- ✅ Integración con Dynamic.xyz para wallet connection
- ✅ Sistema de escrow para fondos
- ✅ Milestone-based funding (all-or-nothing)
- ✅ Monorepo estructurado profesionalmente

Este proyecto sirve como inspiración y guía para desarrolladores que quieren aprender a construir en Solana.

Ver [PRD completo](./docs/aidsmash-prd.md) | [Plan del MVP](./docs/mvp-plan.md)

---

## ⚡ Características del MVP

### Para Non-Profits:
- Crear proyectos de fundraising con múltiples milestones
- Definir metas de recaudación en SOL
- Subir evidencia de progreso (enlaces a IPFS/Arweave)
- Recibir fondos automáticamente al completar milestones

### Para Donantes:
- Explorar proyectos activos
- Donar SOL a proyectos
- Seguir progreso de milestones
- Recibir refunds automáticos si el proyecto no alcanza su meta

### Características Técnicas:
- **All-or-Nothing Funding**: 4 semanas para alcanzar la meta
- **Escrow Seguro**: Fondos bloqueados en PDA hasta aprobación
- **Milestone Validation**: Al menos 3 milestones, primer milestone ≤10%
- **Liberación de Fondos**: Automática al completar milestones

---

## 🛠️ Stack Tecnológico

### Blockchain:
- **Solana** (devnet)
- **Anchor Framework** v0.30.1
- **Rust** (stable)

### Frontend:
- **Vite** + **React 18** + **TypeScript**
- **Dynamic.xyz** (wallet connection)
- **@coral-xyz/anchor**
- **TailwindCSS**

### DevOps:
- **Docker** + **Docker Compose**
- **pnpm** (monorepo)

---

## 🐳 Inicio Rápido con Docker

### Prerrequisitos

- [Docker](https://docs.docker.com/get-docker/) instalado
- [Docker Compose](https://docs.docker.com/compose/install/) instalado
- Git

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/aidsmash.git
cd aidsmash
```

### 2. Construir y lanzar el contenedor

```bash
# Construir la imagen de Docker
docker-compose build

# Iniciar el contenedor en modo interactivo
docker-compose run --rm dev
```

Esto te dará un shell dentro del contenedor con todas las herramientas instaladas:
- ✅ Rust + Cargo
- ✅ Solana CLI (v1.18.26)
- ✅ Anchor CLI (v0.30.1)
- ✅ Node.js 18 + pnpm

### 3. Verificar instalación

Dentro del contenedor:

```bash
# Verificar Rust
rustc --version

# Verificar Solana
solana --version

# Verificar Anchor
anchor --version

# Verificar Node
node --version
pnpm --version
```

### 4. Crear wallet de desarrollo

```bash
# Crear keypair (dentro del contenedor)
solana-keygen new

# Obtener SOL de testnet
solana airdrop 2
```

---

## 📁 Estructura del Proyecto

```
aidsmash/
├── programs/                # Smart contracts Anchor
│   └── aidsmash/
│       ├── src/
│       │   ├── lib.rs      # Entry point del programa
│       │   ├── state.rs    # Account structures
│       │   └── errors.rs   # Custom errors
│       └── Cargo.toml
├── app/                     # Frontend React
│   ├── src/
│   │   ├── components/     # Componentes React
│   │   ├── hooks/          # Custom hooks
│   │   ├── utils/          # Utilidades
│   │   ├── idl/            # IDL generado por Anchor
│   │   └── App.tsx
│   ├── package.json
│   └── vite.config.ts
├── tests/                   # Tests TypeScript
│   └── aidsmash.ts
├── docs/                    # Documentación
│   ├── aidsmash-prd.md     # PRD completo
│   └── mvp-plan.md         # Plan del MVP
├── Anchor.toml              # Configuración Anchor
├── Dockerfile.dev           # Dockerfile de desarrollo
├── docker-compose.yml       # Docker Compose config
└── package.json             # Workspace root
```

---

## 💻 Desarrollo

### Inicializar el proyecto Anchor

```bash
# Dentro del contenedor Docker
anchor init aidsmash --no-git
cd aidsmash
```

### Build del programa

```bash
# Compilar el programa Solana
anchor build

# Generar IDL (Interface Definition Language)
anchor build
```

### Tests

```bash
# Ejecutar tests de Anchor
anchor test

# Tests con validator local
anchor test --skip-local-validator
```

### Deploy a devnet

```bash
# Configurar para devnet
solana config set --url devnet

# Deploy
anchor deploy
```

### Frontend Development

```bash
# Instalar dependencias (desde /workspace/app)
cd app
pnpm install

# Iniciar dev server (con hot reload)
pnpm dev
```

El frontend estará disponible en `http://localhost:5173` (accesible desde el host)

---

## 🧪 Testing

### Tests del Programa

Los tests usan Anchor's testing framework con TypeScript:

```bash
# Ejecutar todos los tests
anchor test

# Tests específicos
anchor test --skip-deploy
```

### Tests del Frontend

```bash
cd app
pnpm test
```

---

## 📚 Documentación

- **[Product Requirements Document (PRD)](./docs/aidsmash-prd.md)**: Visión completa del proyecto
- **[MVP Plan](./docs/mvp-plan.md)**: Roadmap detallado del MVP
- **Program Documentation**: Ver comentarios en `programs/aidsmash/src/`
- **Frontend Documentation**: Ver README en `app/`

### Recursos Externos

- [Anchor Book](https://www.anchor-lang.com/)
- [Solana Cookbook](https://solanacookbook.com/)
- [Dynamic.xyz Docs](https://docs.dynamic.xyz/)
- [Solana Web3.js](https://solana-labs.github.io/solana-web3.js/)

---

## 🤝 Contribuir

Este es un proyecto de ejemplo educativo. Siéntete libre de:

1. Fork el proyecto
2. Crear tu feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push al branch (`git push origin feature/AmazingFeature`)
5. Abrir un Pull Request

---

## 🔧 Comandos Útiles de Docker

```bash
# Iniciar contenedor en background
docker-compose up -d dev

# Entrar al contenedor corriendo
docker-compose exec dev bash

# Ver logs
docker-compose logs -f dev

# Detener contenedor
docker-compose down

# Rebuild si cambia Dockerfile
docker-compose build --no-cache
```

---

## 📝 Notas de Desarrollo

### Solana Config

El contenedor usa **devnet** por defecto. Para cambiar:

```bash
# Localhost (para local validator)
solana config set --url localhost

# Devnet
solana config set --url devnet

# Mainnet (¡CUIDADO!)
solana config set --url mainnet-beta
```

### Anchor Validator Local

Para desarrollo rápido, puedes usar un validator local:

```bash
# Iniciar validator local
solana-test-validator

# En otra terminal, ejecutar tests
anchor test --skip-local-validator
```

---

## 🎓 Propósito Educativo

Este proyecto está diseñado para:

- ✅ Demostrar patrones de desarrollo en Solana
- ✅ Mostrar integración de Anchor + React
- ✅ Servir como template para proyectos reales
- ✅ Inspirar a desarrolladores a construir en Solana

**No está auditado para producción.** Úsalo como referencia educativa.

---

## 📄 Licencia

MIT License - ver [LICENSE](./LICENSE) para detalles

---

## 🌟 Soporte

Si este proyecto te ayudó, dale una ⭐ en GitHub!

Para preguntas o issues, abre un [GitHub Issue](https://github.com/tu-usuario/aidsmash/issues).

---

**Construido con ❤️ para la comunidad de Solana**