# Plan de MVP para AidSmash
## Versión Simplificada - Solana Monorepo

---

## 🎯 Objetivo del MVP

Crear un MVP funcional que demuestre el **concepto core** de AidSmash: fundraising transparente basado en milestones (hitos) usando Solana blockchain. Este proyecto servirá como ejemplo inspirador para otros desarrolladores que quieran construir en Solana.

---

## 🏗️ Arquitectura Simplificada

### Estructura del Monorepo
```
aidsmash/
├── programs/
│   └── aidsmash/          # Programa Anchor en Rust
│       ├── src/
│       │   ├── lib.rs
│       │   ├── state.rs
│       │   └── errors.rs
│       └── Cargo.toml
├── app/                   # Frontend (Vite + React + TypeScript)
│   ├── src/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── utils/
│   │   └── App.tsx
│   ├── package.json
│   └── vite.config.ts
├── tests/                 # Tests en TypeScript
│   └── aidsmash.ts
├── Anchor.toml
└── package.json
```

---

## 🔑 Características del MVP (Simplificadas)

### 1. Smart Contract (Programa Anchor)

#### Cuentas (Accounts):
- **Platform**: Configuración global de la plataforma
- **Project**: Información del proyecto
  - Creador (non-profit wallet)
  - Meta de fundraising
  - Deadline (4 semanas)
  - Estado (Fundraising, Active, Completed, Failed)
  - Fondos recaudados
  - Array de milestones
- **Milestone**: Hito individual
  - Descripción
  - Porcentaje de fondos asignados
  - Estado (Pending, Submitted, Approved, Rejected)
  - URI de evidencia (IPFS/Arweave)
- **Donation**: Registro de donación individual
  - Donante
  - Proyecto
  - Monto

#### Instrucciones (Instructions):
1. **initialize_platform**: Inicializar la plataforma (admin)
2. **create_project**: Crear un nuevo proyecto con milestones
3. **donate_to_project**: Donar SOL a un proyecto
4. **submit_milestone_evidence**: Subir evidencia de milestone completado
5. **approve_milestone**: Aprobar milestone y liberar fondos (simplificado - solo creador por ahora)
6. **finalize_project**: Finalizar proyecto exitoso
7. **refund_failed_project**: Devolver fondos si no se alcanzó la meta en 4 semanas

### 2. Frontend (React + TypeScript)

#### Páginas principales:
1. **Home**: Ver todos los proyectos activos
2. **Create Project**: Formulario para crear proyecto con milestones
3. **Project Detail**: Ver detalles del proyecto, donar, ver milestones
4. **My Projects**: Ver proyectos creados (para non-profits)
5. **My Donations**: Ver donaciones realizadas

#### Integraciones Web3:
- **Dynamic.xyz** para wallet connection (mejor UX)
- @coral-xyz/anchor para interactuar con el programa
- @solana/web3.js

---

## 📝 Simplificaciones para el MVP

Para mantener el MVP manejable y enfocado, **NO incluiremos** (se pueden agregar después):

❌ Token de gobernanza (governance token)
❌ Pre-submission voting por token holders
❌ Mini-DAOs de donantes para aprobar milestones
❌ Sistema de reputación complejo
❌ Backend separado (ExpressJS/PostgreSQL)
❌ Límites de $500/$1000 según región
❌ Fees de plataforma

### Alternativas Simplificadas:

✅ **Aprobación de milestones**: Solo el creador del proyecto puede marcar milestones como completados (sistema de honor). En v2 se puede agregar votación de donantes.

✅ **Almacenamiento**: Todo on-chain excepto evidencia multimedia (usar IPFS/Arweave URIs).

✅ **Fundraising**: Sistema all-or-nothing simple con deadline de 4 semanas.

✅ **Liberación de fondos**: Automática cuando el creador marca milestone como completado y sube evidencia.

---

## 🚀 Roadmap de Desarrollo

### Fase 1: Setup del Proyecto (Día 1-2)
- [ ] Inicializar proyecto Anchor
- [ ] Configurar estructura de monorepo
- [ ] Setup de Vite + React + TypeScript
- [ ] Configurar Wallet Adapter
- [ ] Crear README básico

### Fase 2: Smart Contract Core (Día 3-7)
- [ ] Definir estructuras de datos (Platform, Project, Milestone, Donation)
- [ ] Implementar `initialize_platform`
- [ ] Implementar `create_project` con validaciones:
  - Al menos 3 milestones
  - Primer milestone ≤ 10% del total
  - Suma de milestones = 100%
- [ ] Implementar `donate_to_project` con escrow
- [ ] Implementar lógica de all-or-nothing funding
- [ ] Tests básicos

### Fase 3: Milestone Management (Día 8-11)
- [ ] Implementar `submit_milestone_evidence`
- [ ] Implementar `approve_milestone` con liberación de fondos
- [ ] Implementar `finalize_project`
- [ ] Implementar `refund_failed_project`
- [ ] Tests de flujo completo

### Fase 4: Frontend Básico (Día 12-17)
- [ ] Página Home con lista de proyectos
- [ ] Página Create Project con formulario multi-step
- [ ] Página Project Detail con:
  - Info del proyecto
  - Barra de progreso de fundraising
  - Botón de donación
  - Lista de milestones con estados
- [ ] Conectar wallet y mostrar balance
- [ ] Integrar todas las instrucciones del programa

### Fase 5: Polish y Documentación (Día 18-21)
- [ ] Mejorar UI/UX básico (Tailwind CSS)
- [ ] Agregar loading states y error handling
- [ ] Testing en devnet
- [ ] Escribir documentación completa:
  - README principal
  - Guía de instalación
  - Guía de uso
  - Arquitectura del programa
- [ ] Crear ejemplo de proyecto demo

---

## 🛠️ Stack Tecnológico

### Blockchain:
- **Solana** (devnet para MVP)
- **Anchor Framework** (v0.30+)
- **Rust** (última versión estable)

### Frontend:
- **Vite** (build tool rápido)
- **React 18** + **TypeScript**
- **Dynamic.xyz** (wallet connection)
- **@coral-xyz/anchor**
- **TailwindCSS** (styling)
- **React Router** (navegación)

### Herramientas:
- **Docker** + **Docker Compose** (entorno de desarrollo aislado)
- **Solana CLI** (v1.18.x)
- **Anchor CLI** (v0.30.1)
- **Rust** (stable)
- **Node.js 18+**
- **pnpm** (package manager para monorepo)

---

## 📊 Flujo de Usuario Básico

### Para Non-Profits:
1. Conectar wallet
2. Crear proyecto con:
   - Título y descripción
   - Meta de fundraising (ej: 10 SOL)
   - 3+ milestones con % de fondos
3. Compartir proyecto
4. Esperar donaciones (4 semanas)
5. Si se alcanza la meta:
   - Completar milestones
   - Subir evidencia (link a IPFS/fotos)
   - Recibir fondos automáticamente

### Para Donantes:
1. Conectar wallet
2. Explorar proyectos activos
3. Ver detalles del proyecto y milestones
4. Donar SOL
5. Seguir progreso de milestones
6. Si el proyecto falla, recibir refund automático

---

## 🔐 Consideraciones de Seguridad

### Para el MVP:
1. **Validaciones on-chain**:
   - Verificar firmantes (signers)
   - Validar estados de proyecto
   - Prevenir reentrancy con checks

2. **Manejo de SOL**:
   - Usar PDAs (Program Derived Addresses) para escrow
   - Validar balances antes de transferencias

3. **Límites**:
   - Max 10 milestones por proyecto (para limitar compute)
   - Descripción/evidencia URIs limitadas en tamaño

### Para Producción (futuro):
- Auditoría de smart contracts
- Rate limiting en frontend
- Implementar mini-DAOs para aprobación de milestones
- Sistema de disputes

---

## 📈 Métricas de Éxito del MVP

1. **Funcionalidad**:
   - ✅ Crear proyecto con milestones
   - ✅ Donar a proyecto
   - ✅ Sistema all-or-nothing funcional
   - ✅ Liberación de fondos por milestone
   - ✅ Refunds automáticos

2. **Código**:
   - ✅ Tests con >80% coverage
   - ✅ Deploy exitoso en devnet
   - ✅ Documentación completa

3. **UX**:
   - ✅ Flujo completo de creador a donante funcional
   - ✅ UI limpia y responsive
   - ✅ Error handling claro

---

## 🎓 Valor Educativo

Este MVP sirve como **ejemplo de proyecto real** en Solana que demuestra:

1. **Anchor Framework**: Uso de macros, PDAs, constraints
2. **Escrow Pattern**: Manejo seguro de fondos
3. **State Management**: Estructuras de datos complejas on-chain
4. **Frontend Web3**: Integración React + Anchor
5. **Testing**: Tests completos en TypeScript
6. **Monorepo**: Estructura de proyecto profesional

---

## 🔄 Próximos Pasos (Post-MVP)

Una vez el MVP esté funcionando, se pueden agregar:

1. **Token de Gobernanza**: Pre-submission voting
2. **Mini-DAOs**: Votación de donantes para aprobar milestones
3. **Sistema de Reputación**: Tracking on-chain de éxito de non-profits
4. **Backend**: API para metadata y búsqueda
5. **IPFS Integration**: Upload directo desde el frontend
6. **Mainnet Deploy**: Después de auditoría
7. **Mobile App**: React Native version

---

## 📚 Recursos y Referencias

- [Anchor Book](https://www.anchor-lang.com/)
- [Solana Cookbook](https://solanacookbook.com/)
- [Solana Web3.js Docs](https://solana-labs.github.io/solana-web3.js/)
- [Wallet Adapter](https://github.com/solana-labs/wallet-adapter)

---

**Última actualización**: 2026-01-23
**Versión**: 1.0 - MVP Plan
