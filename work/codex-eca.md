# Edge Computing Architectures

**Audience:** architects and technical decision makers  
**Format target:** approximately ten A4 pages when exported to PDF  
**Scope:** technical principles, architectural patterns, leading industries, use
cases, and source-backed design guidance. This article intentionally avoids code.

## Abstract

Edge computing is the placement of compute, storage, networking, and application
logic closer to the people, machines, sensors, vehicles, and sites that generate
or consume data. It is not a replacement for cloud computing. It is an
architectural extension of cloud and network systems into a continuum that spans
devices, gateways, enterprise sites, access networks, metro facilities, regional
clouds, and centralized clouds.

The architectural problem is therefore not "cloud or edge?" The practical
question is where each workload function should run, what state it should hold,
how it should fail, how it should be observed, and how it should be governed
across many distributed locations. Recent standards and industry work reinforce
that point. ETSI describes Multi-access Edge Computing (MEC) as an open,
multi-vendor environment for deploying applications across distributed edge
platforms. 3GPP specifies edge capabilities in 5G systems, including edge
application discovery, local traffic steering, and edge management functions.
CNCF's edge-native work emphasizes that edge applications must be designed for
constrained resources, autonomy, scale, portability, and operational variance.
NIST's edge AI work highlights the same tension for machine learning: data is
created at the network edge, but edge learning faces constraints in compute,
connectivity, privacy, and robustness.

This article explains the main edge computing architecture patterns, the design
principles behind them, the protocols and standards architects should recognize,
and the industries where edge architecture is already most important.

## 1. Why Edge Architecture Exists

Centralized cloud platforms are excellent at elastic capacity, managed services,
global coordination, and large-scale data processing. They are weaker when a
system depends on bounded local latency, local data residency, autonomous
operation during network impairment, or local interaction with physical
processes. Edge computing exists because some applications cannot tolerate a
purely centralized control loop.

The most common drivers are:

- **Latency:** Industrial control, robotics, vehicle coordination, interactive
  media, and clinical workflows may need responses closer to milliseconds than
  seconds. 3GPP explicitly frames reduced physical distance as a key reason for
  edge computing in 5G networks.
- **Bandwidth and backhaul cost:** Video analytics, sensor streams, and machine
  telemetry can produce more raw data than is economical or useful to transmit
  continuously to a remote region.
- **Data locality and privacy:** Healthcare, public sector, financial services,
  retail, and manufacturing often need to keep sensitive data within a site,
  jurisdiction, vehicle, or facility.
- **Resilience:** Mines, ships, factories, hospitals, stores, and energy assets
  cannot assume perfect WAN connectivity. They need local behavior that degrades
  safely.
- **Context:** Some decisions require fresh local context: radio conditions,
  shop-floor state, traffic density, inventory, location, device health, or
  current energy load.
- **Operational scale:** Edge sites can number in the hundreds, thousands, or
  millions. The architecture must automate deployment, policy, identity,
  observability, and lifecycle management across heterogeneous hardware.

The consequence is architectural distribution. Edge systems split a workload
across tiers instead of placing all functions in a single cloud region.

## 2. Terminology: Cloud, Edge, Fog, Device, and MEC

Architectural discussions often fail because teams use "edge" for different
locations. A useful vocabulary separates location, ownership, and function.

| Term | Typical location | Architectural role |
| --- | --- | --- |
| Device edge | Sensor, phone, camera, PLC, vehicle ECU, robot, medical device | Capture data, run embedded inference, perform immediate safety or control functions |
| Gateway edge | Industrial PC, local gateway, router, appliance | Aggregate devices, normalize protocols, filter streams, enforce local policy |
| On-premises edge | Factory, hospital, store, branch, stadium, campus | Run site applications, local databases, video analytics, control-plane proxies |
| Access/network edge | 5G RAN edge, central office, cable headend, ISP facility | Host latency-sensitive applications near users; integrate with network exposure, traffic steering, and service discovery |
| Metro/regional edge | Metro data center or regional cloud zone | Place workloads close to a population or market while retaining richer cloud operations |
| Central cloud | Hyperscale or private cloud region | Global control, model training, fleet management, analytics, long-term storage |
| Fog computing | Distributed hierarchy between things and cloud | Broader continuum model emphasizing compute, storage, control, and networking across multiple intermediate tiers |
| MEC | Multi-access Edge Computing | ETSI-standardized edge environment for applications near access networks, not limited to mobile access |

In practice, a system may use several of these tiers at once. For example, a
smart factory may run deterministic control in PLCs, protocol conversion on
gateways, visual inspection on on-premises GPU nodes, fleet management in a
regional cloud, and long-term analytics in a central cloud.

## 3. Core Architectural Layers

Most edge computing architectures can be described using six logical layers.

### 3.1 Device and Sensing Layer

This layer includes sensors, actuators, cameras, mobile devices, meters,
wearables, robots, machines, and embedded controllers. Its architectural
constraints are power, real-time behavior, physical safety, limited memory, and
limited update mechanisms.

The device layer should not be treated as a smaller cloud. Devices often run
firmware or embedded operating systems, use specialized buses and industrial
protocols, and may be deployed for years in difficult physical environments.
Architects should decide which device functions are safety-critical, which are
advisory, and which can be delegated upward to a gateway or cloud service.

### 3.2 Local Connectivity and Protocol Layer

Edge architecture is protocol-rich because it bridges operational technology,
telecom, enterprise IT, and cloud systems. Common protocols and technologies
include MQTT, AMQP, CoAP, HTTP, WebSocket, gRPC, OPC UA, Modbus, PROFINET,
EtherNet/IP, DDS, RTSP, RTP, QUIC, TLS, IPsec, Wi-Fi, Ethernet, private 5G,
public 5G, LoRaWAN, Bluetooth Low Energy, Zigbee, and satellite links.

Architectural design should enumerate protocols, normalize where necessary, and
avoid unnecessary translation in latency-sensitive paths. Protocol gateways are
often critical edge components, but every translation layer adds failure modes,
latency, security policy, and observability requirements.

### 3.3 Edge Platform Layer

The platform layer hosts applications and services. It can be a small container
runtime on a gateway, a Kubernetes cluster in a factory, a telco MEC platform,
a virtualized network function environment, or a specialized appliance.

The platform layer normally provides:

- workload scheduling and lifecycle management;
- identity and secrets handling;
- local storage and caching;
- application networking and service discovery;
- policy enforcement;
- health monitoring and logs;
- update and rollback mechanisms;
- integration with cloud control planes.

CNCF's edge-native guidance is especially relevant here: edge platforms must
support constrained resources, large-scale management, portability with limits,
and applications that can span edge and cloud environments.

### 3.4 Edge Data Layer

Edge data architecture decides what is processed locally, what is cached, what
is synchronized, and what is discarded. This layer may include stream
processors, time-series databases, local object stores, message brokers, model
feature stores, metadata catalogs, and event buffers.

The design principle is to avoid moving raw data without purpose. A camera
system may keep raw video locally for a short retention window, send only events
and thumbnails to the cloud, and upload selected clips for audit. A smart grid
system may process phasor or sensor streams at local or regional edge nodes,
then send aggregated state and anomalies upward. NIST-published work on
AI-assisted wide-area monitoring for power grids illustrates why local and edge
processing are attractive when real-time data volumes stress centralized
analysis.

### 3.5 Control, Management, and Orchestration Layer

The control layer is where many edge projects succeed or fail. Running one edge
site is simple. Running hundreds or thousands of sites is a distributed systems
problem.

Architectural concerns include:

- fleet inventory and desired state;
- zero-touch provisioning;
- policy distribution;
- software supply chain integrity;
- workload placement;
- configuration drift detection;
- remote diagnostics;
- offline operation;
- staged rollouts and rollback;
- certificate and key rotation;
- observability across intermittent links.

3GPP's 5G edge architecture makes this separation visible by distinguishing
application, edge enabler, edge hosting, edge management, and transport layers.
It also defines concepts such as Edge Application Servers, Edge Enabler Servers,
Edge Enabler Clients, Edge Configuration Servers, and local traffic steering.
These are telecom-specific terms, but the underlying architectural problem is
general: clients must discover suitable edge services, traffic must be routed
locally when appropriate, and applications must continue across mobility or
relocation events.

### 3.6 Cloud and Enterprise Integration Layer

The cloud remains essential. It usually hosts global fleet management, identity
roots, large-scale analytics, historical storage, model training, business
systems, digital twins, and cross-site optimization. The enterprise layer
connects edge systems to ERP, MES, EHR, CRM, SIEM, IAM, data lakes, and
governance platforms.

The clean architecture is not edge-only. It is a cloud-edge operating model
where edge sites can act locally but remain governed globally.

## 4. Common Architecture Patterns

### 4.1 Device-to-Cloud with Thin Edge

In this pattern, devices connect through a gateway that performs identity,
protocol translation, buffering, and basic filtering, but most application
logic runs in the cloud.

This is suitable when latency is not strict, connectivity is reliable, and the
number of local decisions is small. Examples include consumer telemetry,
environmental monitoring, simple asset tracking, and noncritical building
management.

The main risk is cloud dependency. If the WAN fails, the local system may lose
functionality unless the gateway has a defined offline mode.

### 4.2 Local-First Edge

The local-first pattern places operational application logic at the site. The
cloud manages the fleet and aggregates data, but the site continues to operate
when disconnected.

This is common in factories, hospitals, mines, ships, retail stores, and energy
facilities. A factory visual inspection system, for example, may run inference
locally beside the production line, reject defective products immediately, store
evidence locally, and later synchronize metrics to cloud analytics.

The main challenge is consistency. Local-first systems need explicit rules for
conflict resolution, stale policies, delayed updates, and local authority.

### 4.3 Network Edge and MEC

The network-edge pattern places workloads in access-network or metro locations.
It is especially relevant for telecom operators, 5G applications, content
delivery, gaming, vehicle-to-everything services, drones, augmented reality,
video analytics, and enterprise private networks.

ETSI MEC is the most prominent standards family for this area. ETSI describes
MEC as providing cloud-computing capabilities and an IT service environment at
the edge of a network, with deployment options that range from on-premises edge
to network edge and with federation across service providers and cloud
providers. 3GPP complements this with 5G system architecture and an edge
enabler layer that helps applications discover and consume edge services.

The main challenge is multi-party coordination. The application owner, telecom
operator, cloud provider, enterprise, and device owner may all control different
parts of the path.

### 4.4 Hierarchical Edge

Hierarchical edge uses multiple tiers: device, gateway, site, metro, region, and
cloud. Each tier has a different function and authority.

Examples include smart cities, energy grids, transportation networks, and
large-scale retail. A city traffic system may process camera feeds at an
intersection, coordinate corridors at a district edge, optimize policy at a city
operations center, and store long-term planning data in the cloud.

The main design issue is placement. Architects must decide which tier owns
real-time control, local aggregation, privacy filtering, cross-site
optimization, and historical learning.

### 4.5 Edge AI and Federated Learning

Edge AI places inference, feature extraction, or learning close to data sources.
It is often used for visual inspection, predictive maintenance, medical imaging
triage, speech processing, anomaly detection, vehicle perception, and robotics.

NIST's edge AI program notes that data is increasingly created at network edges
and cannot all be sent to the cloud. It also identifies major challenges:
resource constraints, non-IID data distributions, privacy requirements,
communication limits, and security vulnerabilities.

Architecturally, edge AI needs:

- model distribution and version control;
- hardware-aware placement;
- local inference monitoring;
- drift detection;
- privacy-preserving data handling;
- retraining workflows;
- rollback when a model performs poorly;
- clear accountability for automated decisions.

The main risk is treating model deployment as a file-copy problem. It is a
lifecycle and governance problem.

### 4.6 Edge-Cloud Continuum

Recent research describes cloud and edge as an integrated continuum rather than
separate platforms. Surveys on cloud-to-edge collaboration discuss
thing-edge, edge-cloud, edge-edge, and thing-edge-cloud collaboration patterns.
This framing is useful because it focuses on dynamic allocation of compute,
caching, communication, and storage across tiers.

The continuum pattern is suitable when demand changes by time, location, user
density, network condition, or energy cost. Examples include large events,
connected vehicles, public safety, metaverse-like interactive services, and
distributed AI workloads.

The main challenge is policy. If placement changes dynamically, the system must
still satisfy latency, privacy, cost, energy, and resilience constraints.

## 5. Architectural Principles

### 5.1 Place Workloads by Constraint, Not Fashion

An edge placement decision should be justified by a concrete constraint:
latency, autonomy, bandwidth, privacy, physical process coupling, cost, or
regulatory locality. If no constraint requires local placement, cloud placement
may be simpler and more reliable.

### 5.2 Keep Control Loops Local When Safety or Time Requires It

Closed-loop control for machines, vehicles, robotics, or clinical operations
should not depend on distant cloud round trips. Local systems should handle the
immediate decision, while cloud systems handle optimization, learning, audit,
and coordination.

### 5.3 Design for Intermittent Connectivity

Edge nodes must often operate through packet loss, weak backhaul, planned
maintenance, or full disconnection. Applications should define offline behavior:
what continues, what stops, what queues, what expires, and what requires human
approval.

### 5.4 Minimize Raw Data Movement

Move signals, events, aggregates, features, and exceptions when possible. Move
raw data only when it is needed for audit, training, forensics, or downstream
analysis. This reduces bandwidth cost and limits privacy exposure.

### 5.5 Treat Edge Sites as Hostile or Semi-Trusted

Many edge nodes sit in stores, vehicles, cabinets, factories, or public spaces.
They may be physically accessible to attackers. Architectures should assume
tamper risk and use secure boot, hardware roots of trust where appropriate,
disk encryption, measured updates, least privilege, certificate-based identity,
remote attestation where available, and short-lived credentials.

### 5.6 Make Operations Fleet-Oriented

Manual administration does not scale. Edge architecture needs desired-state
management, staged rollouts, health scoring, automated rollback, policy
templates, inventory, and remote diagnostics. Every edge node should be
replaceable without artisanal reconstruction.

### 5.7 Separate Data Plane, Control Plane, and Management Plane

The data plane handles application traffic and local processing. The control
plane decides placement, discovery, routing, and desired state. The management
plane handles lifecycle, inventory, monitoring, and policy. Confusing these
planes creates fragile systems and unclear security boundaries.

### 5.8 Prefer Open Interfaces Where Ecosystems Matter

Edge systems frequently span multiple vendors and owners. Standards and open
interfaces reduce lock-in and integration risk, especially in telecom MEC,
industrial automation, smart cities, and connected vehicle ecosystems.

## 6. Security and Governance Architecture

Edge security extends cloud security into less controlled environments.
Architects should address the following domains explicitly.

| Domain | Architectural requirement | Example |
| --- | --- | --- |
| Identity | Every device, node, workload, and operator has a verifiable identity | X.509 certificates for gateways and mutual TLS for service calls |
| Supply chain | Software and models are signed, traceable, and deployable by policy | Signed container images and signed ML model artifacts |
| Physical risk | Nodes tolerate theft, tampering, and unplanned replacement | Encrypted disks and hardware-backed keys |
| Network exposure | Local services expose only required interfaces | Segmented OT network with controlled northbound data export |
| Data governance | Sensitive data is classified before movement | Medical images processed locally, metadata exported centrally |
| Observability | Security events survive intermittent links | Local buffering of audit logs with later forwarding to SIEM |
| Resilience | Sites degrade safely | Factory line continues with last approved model if WAN is down |

Security governance must also cover who may deploy workloads to an edge site,
who may access local data, how emergency access is audited, and how regulatory
boundaries are enforced.

## 7. Leading Use Cases and Industries

### 7.1 Manufacturing and Industrial Automation

Manufacturing is one of the strongest edge domains because it combines
real-time processes, expensive downtime, high-volume sensor data, and site
autonomy.

Examples:

- **Visual quality inspection:** Cameras and local GPUs inspect products on the
  line. Only defects, metrics, and sample evidence are sent to the cloud.
- **Predictive maintenance:** Vibration, acoustic, and thermal data are
  processed locally to detect bearing wear or motor anomalies.
- **Digital work cells:** Robots, PLCs, and edge servers coordinate with local
  safety constraints while enterprise systems receive production summaries.
- **Private 5G factories:** Wireless machines and mobile robots use local
  breakout and edge applications for low-latency coordination.

Architecture emphasis: deterministic control stays local; analytics and
optimization synchronize upward.

### 7.2 Telecommunications and 5G Services

Telecom edge architecture is shaped by MEC, 5G core functions, user-plane
selection, application discovery, service continuity, and federation across
operators.

Examples:

- **AR/VR rendering assistance:** Edge servers reduce motion-to-photon latency
  by placing compute near users.
- **Cloud gaming:** Rendering or session acceleration runs in metro edge sites.
- **Video optimization:** Content is cached and adapted near access networks.
- **Enterprise private networks:** A campus runs local application servers
  integrated with private 5G and enterprise systems.
- **V2X support:** Roadside and network-edge applications assist vehicles with
  local hazard awareness or traffic coordination.

Architecture emphasis: service discovery, local traffic steering, session
continuity, and ecosystem interoperability.

### 7.3 Healthcare

Healthcare edge systems must balance latency, privacy, regulatory compliance,
clinical safety, and integration with hospital systems.

Examples:

- **Medical imaging triage:** Imaging devices or local hospital servers run
  inference to flag urgent cases while retaining protected data on premises.
- **Operating room analytics:** Local systems process video, telemetry, and
  device data without depending on external connectivity.
- **Remote patient monitoring:** Gateways filter wearable data and escalate
  anomalies.
- **Hospital resilience:** Critical systems continue locally during WAN outages.

Architecture emphasis: data locality, auditability, clinical governance, and
safe degradation.

### 7.4 Retail, Hospitality, and Branch Operations

Retail edge architecture is driven by many distributed sites, local customer
experience, video, inventory, and payment resilience.

Examples:

- **Computer vision for shelves:** Local video analytics detect stockouts,
  queue length, or planogram drift.
- **Point-of-sale continuity:** Stores continue limited operations during WAN
  outages.
- **Loss prevention:** Events are detected locally and summarized centrally.
- **Personalized in-store experiences:** Local systems react to inventory,
  location, and customer context without sending all raw data to the cloud.

Architecture emphasis: fleet management, low-touch operations, privacy, and
cost-effective hardware.

### 7.5 Energy, Utilities, and Smart Grid

Energy systems need distributed intelligence because generation, storage,
loads, and grid sensors are geographically distributed.

Examples:

- **Substation analytics:** Edge nodes detect anomalies from local telemetry.
- **Distributed energy resource coordination:** Solar, batteries, and loads are
  optimized locally and coordinated regionally.
- **Wide-area monitoring:** Regional edge processing reduces delay and data
  volume for grid events.
- **Field asset inspection:** Drones and mobile edge systems process imagery
  near the inspection site.

Architecture emphasis: resilience, deterministic response, security, and
hierarchical control.

### 7.6 Transportation, Automotive, and Logistics

Mobility makes edge placement dynamic. Vehicles, depots, roads, ports, and
warehouses all become computing locations.

Examples:

- **Connected vehicles:** Applications use roadside or network edge servers for
  hazard alerts and cooperative perception.
- **Ports and warehouses:** Local edge systems coordinate cranes, automated
  guided vehicles, cameras, and inventory systems.
- **Fleet maintenance:** Vehicle telemetry is analyzed at depots and summarized
  centrally.
- **Rail and aviation operations:** Local processing supports safety,
  maintenance, and passenger operations where connectivity may vary.

Architecture emphasis: mobility, intermittent links, location-aware service
discovery, and safety boundaries.

### 7.7 Smart Cities and Public Sector

Smart city systems require cross-agency governance and careful privacy design.

Examples:

- **Traffic optimization:** Intersections process local sensor data and
  coordinate with district controllers.
- **Public safety video:** Local analytics detect events while limiting raw
  video retention and access.
- **Environmental monitoring:** Distributed sensors detect air quality, flood
  risk, or noise patterns.
- **Emergency response:** Temporary edge nodes support communications and data
  processing during incidents.

Architecture emphasis: governance, interoperability, public trust, and
multi-tier coordination.

### 7.8 Media, Entertainment, and Live Events

Media edge architectures manage high bandwidth and interactive latency.

Examples:

- **Live event production:** Local edge systems process camera feeds, graphics,
  and streams before cloud distribution.
- **Interactive fan experiences:** Stadium applications respond locally to
  crowd density, location, and media demand.
- **Content delivery:** Popular content is cached close to users.
- **Real-time translation or captioning:** Local inference reduces latency and
  preserves event continuity.

Architecture emphasis: bandwidth reduction, burst capacity, and user proximity.

## 8. Meaningful Trade-Offs

Edge architecture introduces value, but also cost and complexity.

| Design choice | Benefit | Cost or risk |
| --- | --- | --- |
| More local processing | Lower latency and less backhaul | More distributed operations and hardware lifecycle work |
| Local data retention | Privacy and resilience | Data governance must cover many sites |
| Dynamic workload placement | Better resource use | Harder policy, testing, and troubleshooting |
| Vendor-specific edge platform | Faster integration | Lock-in and migration risk |
| Open, portable platform | Ecosystem flexibility | More integration responsibility |
| Edge AI | Faster decisions and less data movement | Model drift, hardware variance, and governance complexity |
| Full offline autonomy | Strong resilience | Conflict handling and stale policy risk |

The architectural discipline is to accept complexity only where it buys a
measurable constraint improvement.

## 9. Reference Architecture

A general-purpose edge architecture for an enterprise or public-sector system
can be organized as follows:

1. **Device tier:** sensors, machines, cameras, controllers, phones, vehicles,
   or medical devices.
2. **Gateway tier:** protocol normalization, local buffering, device identity,
   filtering, and basic rule execution.
3. **Site edge tier:** local applications, stream processing, inference,
   short-term storage, local dashboards, and site policy.
4. **Network or metro edge tier:** latency-sensitive shared services,
   multi-site aggregation, MEC workloads, content caching, and mobility support.
5. **Cloud tier:** global management, analytics, model training, long-term
   storage, enterprise integration, and governance.
6. **Operations plane:** inventory, deployment, monitoring, security policy,
   audit, update management, and incident response across all tiers.

This reference architecture should be adapted by constraint. A small retail
store may need only gateway, site, and cloud. A connected-vehicle system may
need device, roadside, network edge, regional, and cloud tiers. A hospital may
emphasize on-premises autonomy and data locality more than network-edge
federation.

## 10. Evaluation Checklist for Architects

Before approving an edge architecture, architects should be able to answer:

1. Which workload functions require local placement, and why?
2. What is the maximum acceptable latency for each control loop?
3. Which data must remain local, and for how long?
4. What continues during WAN outage, and what stops?
5. How are devices, nodes, workloads, operators, and models identified?
6. How are software and model updates signed, staged, verified, and rolled back?
7. How is observability preserved when links are intermittent?
8. How is local state reconciled with cloud state?
9. What protocols cross each trust boundary?
10. How are edge nodes replaced without manual reconstruction?
11. Which standards or open interfaces matter for the ecosystem?
12. What is the total operational cost per site over the system lifetime?

## 11. Conclusion

Edge computing architecture is the discipline of distributing digital systems
across the physical world without losing governance, security, or operational
control. Its value is clearest where latency, autonomy, bandwidth, privacy,
resilience, or local context materially changes the system outcome.

The best architectures are not defined by placing everything at the edge. They
are defined by deliberate placement. Safety-critical and time-critical loops run
locally. High-volume raw data is filtered near its source. Sensitive data is
kept within appropriate boundaries. Fleet operations are automated. Cloud
systems remain responsible for global coordination, analytics, governance, and
continuous improvement.

For architects, the practical target is a managed cloud-edge continuum: local
enough to act, connected enough to learn, standardized enough to integrate, and
secure enough to trust.

## Selected Sources

- ETSI, ["ICT infrastructure and operations"](https://www.etsi.org/technologies/ict-infrastructure-operations/), accessed
  April 23, 2026.
- ETSI, ["ISG MEC"](https://www.etsi.org/technical-groups/mec/), technical group overview,
  accessed April 23, 2026.
- 3GPP, ["Edge Computing"](https://www.3gpp.org/technologies/edge-computing), June 5, 2023,
  accessed April 23, 2026.
- 3GPP, "3GPP EDGEAPP: Roaming, Federation and Edge Node Sharing,"
  September 19, 2023, accessed April 23, 2026.
  [Source](https://www.3gpp.org/technologies/edge-app).
- CNCF, ["Edge Native Applications Principles Whitepaper"](https://www.cncf.io/reports/edge-native-applications-principles-whitepaper/),
  March 9, 2023, accessed April 23, 2026.
- CNCF, ["Edge Native Application Design Behaviors Whitepaper"](https://www.cncf.io/reports/edge-native-application-design-behaviors-whitepaper/),
  January 18, 2024, accessed April 23, 2026.
- NIST, ["Edge AI"](https://www.nist.gov/programs-projects/edge-ai), updated March 26, 2025,
  accessed April 23, 2026.
- Bin Hu and Hamid Gharavi, "Artificial Intelligence-Assisted Edge Computing
  for Wide Area Monitoring," NIST / IEEE Open Journal of the Communications
  Society, 2023. [Source](https://www.nist.gov/publications/artificial-intelligence-assisted-edge-computing-wide-area-monitoring).
- Nour Alhuda Sulieman, Lorenzo Ricciardi Celsi, Wei Li, Albert Zomaya, and
  Massimo Villari, "Edge-Oriented Computing: A Survey on Research and Use
  Cases," *Energies*, 2022. [DOI](https://doi.org/10.3390/en15020452).
- Liming Cao et al., "Cost optimization in edge computing: a survey,"
  *Artificial Intelligence Review*, 2024.
  [DOI](https://doi.org/10.1007/s10462-024-10947-4).
- "A survey on integrated computing, caching, and communication in the
  cloud-to-edge continuum," *Computer Communications*, 2024.
  [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0140366424000847).
