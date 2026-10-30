# Julián Zabala

**Backend Engineer** · REST APIs, integraciones empresariales y consistencia de datos.

Licenciado en Sistemas (UNNOBA) · Junín, Buenos Aires · Remoto UTC-3

6 años en software (2020–hoy), 4+ en desarrollo web con Node.js, Angular y SQL Server / PostgreSQL.

[![Portfolio](https://img.shields.io/badge/Portfolio-licenciadojulianzabala.com.ar-D9A441?style=flat-square&logoColor=white)](https://www.licenciadojulianzabala.com.ar/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-julian--zabala-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/julian-zabala-0a000b1b3/)
[![Email](https://img.shields.io/badge/Email-zabalajulian98@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:zabalajulian98@gmail.com)

---

### En qué trabajo

Diseño backends que tienen que seguir siendo correctos cuando el sistema del otro lado deja de
responder. En la empresa **KipBip** (https://kipbip.com/) mantengo 3 productos en producción: el core sistema con su mismo nombre 'KipBip',
`pk-connector`, la plataforma de integración on-premise con SAP S/4HANA, Solera RNA y
Descartes Roadnet y 'pk-metricas' sistema interno que recopila información para la toma de decisiones.

Mi día a día es mensajería asíncrona, garantías de entrega y transaccionalidad:
RabbitMQ con Dead Letter Queues, Transactional Outbox, CQRS-lite, cache-aside en Redis
y aislamiento transaccional en SQL Server y PostgreSQL.

> La mayor parte de mi código vive en repositorios privados de empresa.
> Lo que sí es público son las decisiones: cada caso de mi
> **[portfolio](https://www.licenciadojulianzabala.com.ar/)** documenta el problema,
> la topología del sistema, el trade-off que elegí y el costo que acepté.

---

### `pk-connector` — el sistema del que más aprendí

Motor de integración entre ERPs corporativos on-premise y nuestra plataforma de ruteo.

```
ERPs on-premise → Strategy + Factory → RabbitMQ → Workers → SSE (telemetría)
                                          ↓ error transitorio
                              DLQ → cola de delay (TTL) → reintento
```

- **Strategy + Factory** para sumar un ERP nuevo sin tocar el núcleo.
- **Errores transitorios vs. terminales:** un timeout o un 429/5xx del ERP pasa por la DLQ y
  reintenta con backoff exponencial (cola de delay con TTL en el broker, sin bloquear el
  prefetch); un error terminal no se reintenta y queda registrado como fallido.
- **Credenciales** de los ERPs cifradas con AES-256-GCM.
- **Server-Sent Events** para telemetría del pipeline, sin el overhead de WebSockets
  bidireccionales.

---

### Cómo decido

| Decisión | Por qué | Qué cuesta |
|---|---|---|
| At-least-once + idempotencia | *Exactly-once* no existe entre una base y un broker | Estado extra que mantener |
| Monolito modular antes que microservicios | Límites claros valen más que despliegues independientes | La disciplina depende del code review |
| Distinguir error transitorio de terminal | Un timeout se cura reintentando; un payload inválido no | Hay que clasificar cada error a mano |
| Abstraer donde el cambio ya ocurrió | Strategy en el conector porque cada cliente trae un ERP nuevo | Si me equivoco, refactorizo después |
| Testear comportamiento, no implementación | Una suite que se rompe en cada refactor deja de ser una red | Menos cobertura de UI |

---

### Stack

**Core** · TypeScript · Node.js · Express · class-validator · tsyringe (IoC)

**Datos** · SQL Server · PostgreSQL · Redis · Sequelize · Prisma

**Asincronía** · RabbitMQ (DLQ) · Transactional Outbox · BullMQ · Server-Sent Events

**Frontend** · Angular 17 (RxJS, Signals) · React 19 (TanStack Query, Zustand) · Tailwind

**Calidad** · Jest · SuperTest · Sentry · ESLint · Husky

**Infra** · Docker · GitHub Actions · GitLab CI · AWS (EC2, S3, Route 53)

**Arquitectura** · SOLID · Clean / Layered · DDD-lite · CQRS-lite · Unit of Work · RBAC

**Monitorización y Observabilidad (incorporando en proyecto nuevo)** · Prometheus · Grafana.
---

### Proyectos propios

| Proyecto | Qué es | Foco técnico |
|---|---|---|
| **GeCe Comercial** | ERP/POS para comercios, primera versión en producción | Transactional Outbox con `FOR UPDATE SKIP LOCKED`, bounded contexts, Argon2 con fallback legacy |
| **VínculoSalud** | Gestión de turnos para el sector salud | Aislamiento Serializable contra solapamiento de turnos, Unit of Work, RBAC granular |
| **Portfolio** | Mi sitio personal | React 19 + Vite + TypeScript, prerenderizado para SEO, con vistas adaptadas al perfil del visitante y diagramas SVG propios |

---

### Disponibilidad

**Software Engineer | Backend / Full Stack Developer**

Más de 6 años de experiencia en desarrollo de software. Interesado en nuevos desafíos profesionales, preferentemente en modalidad remota (UTC-3), dentro de equipos de ingeniería que valoren la colaboración, las buenas prácticas y la calidad del software.

Me interesa formar parte de equipos de ingeniería de software, participar en la construcción de soluciones desde el análisis de requerimientos hasta su puesta en producción y trabajar en entornos colaborativos, con buenas prácticas, responsabilidades definidas y foco en la calidad del software.

Busco seguir creciendo profesionalmente, aportar mi experiencia y aprender de otros perfiles técnicos.

📬 **[zabalajulian98@gmail.com](mailto:zabalajulian98@gmail.com)**
