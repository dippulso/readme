Use a prompt like this. I would make the coding agent treat the sketch as a **functional Angular diagram editor**, not merely try to reproduce it with HTML/CSS.

> I need you to implement an **Angular frontend architecture/network diagram component** based on the attached/reference sketch.
>
> The visual structure should resemble the sketch, but the result must look like a **modern production UI built with ngDiagram**, not a hand-drawn image.
>
> ## Main requirement
>
> Build an interactive Angular component that visualizes this topology:
>
> ```text
> Actor/User
>      │
>      ├──── Mobile ────┐
>      │                │
>      └──── Web App ───┼──> WAF ───> Kubernetes ───> PostgreSQL
>                       │                          TCP 5432
>                       │
> Internet              DMZ                     LAN
> ```
>
> The screen must clearly show three large network/security zones:
>
> ```text
> ┌──────────── INTERNET ───────────┬──────────── DMZ ────────────┬────────── LAN ──────────┐
> │                                │                             │                         │
> │      Mobile                    │      WAF                    │      Internal Server    │
> │      IP                        │                             │                         │
> │                               │           Kubernetes        │      Internal Server    │
> │      Web App                   │           Cluster           │                         │
> │      IP                        │                             │                         │
> │                               │           IP                │      PostgreSQL         │
> │                               │                             │      198.x.x.x          │
> │                               │                  ──────────────── TCP :5432           │
> └───────────────────────────────┴─────────────────────────────┴─────────────────────────┘
>
> Actor/User sits OUTSIDE the Internet boundary on the far left.
> ```
>
> ## Technology
>
> Use:
>
> - Angular
> - TypeScript
> - SCSS
> - the **ngDiagram/diagram library already installed in the project**
> - do NOT replace the existing diagram library with another package
> - inspect the existing project/package.json and existing diagram components before implementing anything
>
> If the library supports groups, containers, swimlanes, nested nodes, custom node templates, ports or annotations, use those features rather than faking the whole diagram with absolute-positioned HTML.
>
> Keep the graph topology/data separate from its visual templates.
>
> ## Component
>
> Create a reusable component similar to:
>
> ```text
> NetworkArchitectureDiagramComponent
> ```
>
> Prefer separating the implementation into:
>
> ```text
> network-architecture-diagram.component.ts
> network-architecture-diagram.component.html
> network-architecture-diagram.component.scss
> network-architecture-diagram.models.ts
> ```
>
> Adapt filenames to the existing project conventions if necessary.
>
> ---
>
> # Visual design
>
> Do NOT imitate the hand-written appearance of the reference.
>
> Convert it into a clean infrastructure-management/dashboard UI.
>
> Use:
>
> - white/light-gray canvas
> - subtle grid or dot-grid background
> - rounded cards
> - subtle borders
> - very light shadows
> - professional typography
> - restrained enterprise colors
> - generous whitespace
>
> The UI should feel similar to:
>
> - cloud architecture tools
> - Kubernetes dashboards
> - infrastructure topology viewers
> - modern network management tools
>
> It should NOT look like PowerPoint or a static flowchart.
>
> ---
>
> # Network zones
>
> Create three visually distinct large containers:
>
> ### INTERNET
>
> Left zone.
>
> Header:
>
> ```text
> INTERNET
> Public Network
> ```
>
> Give the container a subtle blue treatment.
>
> Contains:
>
> ### Mobile
>
> Card content:
>
> ```text
> Mobile
> Public Endpoint
>
> IP
> 203.0.113.10
> ```
>
> Use an appropriate smartphone/client icon.
>
> ### Web App
>
> ```text
> Web Application
> Public Endpoint
>
> IP
> 203.0.113.20
> ```
>
> Use a browser/web icon.
>
> ---
>
> # Actor
>
> On the far left, OUTSIDE all zones:
>
> ```text
> User
> External Actor
> ```
>
> Use a user/person icon.
>
> Create connections:
>
> ```text
> User -> Mobile
> User -> Web Application
> ```
>
> ---
>
> # DMZ
>
> Middle zone.
>
> Header:
>
> ```text
> DMZ
> Demilitarized Zone
> ```
>
> Give it a subtle orange/amber security-oriented treatment.
>
> Contains:
>
> ## WAF
>
> ```text
> Web Application Firewall
> WAF
>
> IP
> 10.10.0.10
> ```
>
> Use a shield/firewall icon.
>
> Connections:
>
> ```text
> Mobile -> WAF
> Web Application -> WAF
> ```
>
> These connections may show:
>
> ```text
> HTTPS
> :443
> ```
>
> ---
>
> ## Kubernetes
>
> Create a noticeably larger node/container:
>
> ```text
> Kubernetes
> Application Cluster
>
> 10.20.0.0/24
> ```
>
> Use a Kubernetes/cloud/cluster icon.
>
> WAF connects to Kubernetes:
>
> ```text
> WAF
>     |
>     | HTTPS :443
>     v
> Kubernetes
> ```
>
> The Kubernetes card should visually communicate that it represents a cluster rather than a normal machine.
>
> Optionally show a small secondary line:
>
> ```text
> 3 Nodes
> ```
>
> or
>
> ```text
> K8s Cluster
> ```
>
> ---
>
> # LAN
>
> Right zone.
>
> Header:
>
> ```text
> LAN
> Internal Network
> ```
>
> Give it a subtle green treatment.
>
> Add two internal server nodes:
>
> ```text
> Internal Service A
> 10.30.0.11
> ```
>
> ```text
> Internal Service B
> 10.30.0.12
> ```
>
> Use server/service icons.
>
> They can initially be unconnected, matching the rough reference.
>
> At the bottom-right add:
>
> ```text
> PostgreSQL
> Database
>
> 198.x.x.x
> :5432
> ```
>
> Use a database icon.
>
> Create:
>
> ```text
> Kubernetes ────────────────> PostgreSQL
> ```
>
> The edge must prominently display:
>
> ```text
> TCP :5432
> ```
>
> or
>
> ```text
> PostgreSQL
> TCP 5432
> ```
>
> ---
>
> # Node design
>
> Do not use plain rectangles.
>
> Every infrastructure node should be a reusable custom node card.
>
> Example appearance:
>
> ```text
> ┌──────────────────────────────┐
> │ [icon] Web Application      │
> │        Public Endpoint      │
> │                              │
> │ IP                           │
> │ 203.0.113.20                │
> └──────────────────────────────┘
> ```
>
> Cards should have:
>
> - 8–12px corner radius
> - subtle border
> - icon
> - primary name
> - secondary type
> - optional metadata
> - status indicator when appropriate
>
> For Kubernetes:
>
> ```text
> ┌──────────────────────────────────┐
> │ Kubernetes Cluster               │
> │ Application Runtime              │
> │                                  │
> │  ● node-01   ● node-02   ● node-03
> │                                  │
> │ Network                          │
> │ 10.20.0.0/24                    │
> └──────────────────────────────────┘
> ```
>
> Do not overcomplicate the internal Kubernetes visualization.
>
> ---
>
> # Connections
>
> Make edges clean and professional.
>
> Prefer:
>
> - orthogonal/elbow connectors
> - arrow at target
> - approximately 1.5–2px line
> - soft neutral color
>
> Avoid diagonal lines whenever possible.
>
> Example:
>
> ```text
> User
>    ├────────> Mobile
>    └────────> Web App
>
> Mobile ─────┐
>             ├────> WAF ─────> Kubernetes ─────> PostgreSQL
> Web App ────┘                            TCP :5432
> ```
>
> Labels should appear on connections inside small label pills:
>
> ```text
> HTTPS :443
> ```
>
> ```text
> TCP :5432
> ```
>
> ---
>
> # Ports
>
> If ngDiagram supports connection ports/handles, use explicit ports.
>
> For example:
>
> ```text
>       incoming
>          ↓
>     ┌─────────┐
> in →│   WAF   │→ out
>     └─────────┘
> ```
>
> Use logical IDs such as:
>
> ```typescript
> input
> output
> north
> south
> ```
>
> rather than connecting edges to arbitrary coordinates.
>
> ---
>
> # Data-driven model
>
> Do NOT hardcode each node independently in HTML.
>
> Represent the graph through TypeScript data.
>
> For example:
>
> ```typescript
> interface ArchitectureNode {
>   id: string;
>   name: string;
>   type:
>     | 'actor'
>     | 'mobile'
>     | 'web'
>     | 'waf'
>     | 'kubernetes'
>     | 'server'
>     | 'database';
>   zone?: 'internet' | 'dmz' | 'lan';
>   ip?: string;
>   subtitle?: string;
>   status?: 'healthy' | 'warning' | 'offline';
>   x: number;
>   y: number;
> }
>
> interface ArchitectureEdge {
>   id: string;
>   source: string;
>   target: string;
>   protocol?: string;
>   port?: number;
> }
> ```
>
> Use approximately:
>
> ```typescript
> user
>
> mobile
> webapp
>
> waf
> kubernetes
>
> internal-service-a
> internal-service-b
> postgres
> ```
>
> ---
>
> # Layout
>
> Initial positions should closely correspond to:
>
> ```text
>      USER
>        │
>        ├──── MOBILE ──────┐
>        │                  │
>        └──── WEB APP ─────┤
>                           v
>                INTERNET  WAF
>                           │
>                           v
>                     KUBERNETES
>                           │
>                           │ TCP :5432
>                           │
>                           └────────────────────────> POSTGRES
>
>                DMZ                                LAN
> ```
>
> The overall direction of traffic is:
>
> ```text
> LEFT → RIGHT
> ```
>
> Do not use an automatic layout if it causes the three network zones to become mixed together.
>
> Explicitly position the initial nodes if necessary.
>
> ---
>
> # Interaction
>
> I want this to behave like an actual diagramming component.
>
> Implement:
>
> - node dragging
> - canvas panning
> - zoom
> - mouse-wheel zoom where appropriate
> - fit-to-screen
> - reset view
> - node selection
> - selected node highlighting
> - connection highlighting
> - hover states
>
> Add a small floating toolbar:
>
> ```text
> [ + ] [ - ] [ Fit ] [ Reset ]
> ```
>
> Keep it visually unobtrusive.
>
> If supported easily by the existing library, also allow:
>
> ```text
> Ctrl + mouse wheel -> zoom
> Space + drag -> pan
> ```
>
> Do not implement these manually if the diagram library already provides them.
>
> ---
>
> # Details panel
>
> When a node is clicked, display a small right-side inspector panel.
>
> Example:
>
> ```text
> Kubernetes
>
> Type
> Application Cluster
>
> Network
> 10.20.0.0/24
>
> Zone
> DMZ
>
> Status
> Healthy
>
> Connections
> WAF -> Kubernetes
> Kubernetes -> PostgreSQL
> ```
>
> Clicking empty canvas should deselect the node and hide/collapse the inspector.
>
> This should be relatively lightweight; the diagram itself remains the main focus.
>
> ---
>
> # Security-zone appearance
>
> Network zones must be visually obvious without overwhelming the diagram.
>
> For example:
>
> ```text
> INTERNET
> ┌────────────────────────────┐
> │                            │
> │                            │
> └────────────────────────────┘
>
> DMZ
> ┌────────────────────────────┐
> │                            │
> │                            │
> └────────────────────────────┘
>
> LAN
> ┌────────────────────────────┐
> │                            │
> │                            │
> └────────────────────────────┘
> ```
>
> They should behave like background/group containers.
>
> Nodes should render above the zone background.
>
> If the diagram library supports parent/group nodes, use that functionality.
>
> Otherwise implement zones as a dedicated background layer in the diagram rather than normal foreground cards.
>
> ---
>
> # Responsive behavior
>
> The diagram should work reasonably at:
>
> ```text
> 1920 × 1080
> 1440 × 900
> 1366 × 768
> ```
>
> The component should fill its parent:
>
> ```css
> width: 100%;
> height: 100%;
> min-height: 650px;
> ```
>
> Do not allow normal page scrolling to interfere with diagram panning.
>
> ---
>
> # Important implementation rules
>
> Before coding:
>
> 1. Inspect `package.json`.
> 2. Find which ngDiagram/diagram package is actually installed.
> 3. Search the codebase for existing usages of that library.
> 4. Follow the existing Angular version, standalone/module conventions and coding style.
> 5. Reuse existing design-system components/icons where available.
>
> Do not invent APIs for the diagram package.
>
> If you are unsure about an API, inspect the installed typings/package source before using it.
>
> Do not replace the diagram library just because another library is easier.
>
> Do not render the architecture as one SVG/image.
>
> Do not reproduce the reference as a static screenshot.
>
> I need actual nodes, connectors, containers and interactions.
>
> ---
>
> # Code quality
>
> Keep:
>
> ```text
> graph data
> diagram configuration
> node rendering
> edge rendering
> interaction state
> ```
>
> reasonably separated.
>
> Prefer small helper functions instead of a giant component initialization method.
>
> Use strong TypeScript types and avoid `any`.
>
> Use Angular signals if this project already uses signals; otherwise follow the project's existing state-management style.
>
> Do not introduce unnecessary dependencies.
>
> ---
>
> # Expected final appearance
>
> The final result should conceptually look like:
>
> ```text
>                         NETWORK ARCHITECTURE
>
>               INTERNET               DMZ                        LAN
>       ╭────────────────────╮ ╭──────────────────────╮ ╭──────────────────────────╮
>       │                    │ │                      │ │                          │
>       │ ┌──────────────┐   │ │ ┌──────────────┐     │ │ ┌────────────────────┐   │
> USER ─┼→│ 📱 Mobile    │───┼─┼→│ 🛡 WAF      │     │ │ │ Internal Service A │   │
>   │   │ └──────────────┘   │ │ └──────┬───────┘     │ │ └────────────────────┘   │
>   │   │                    │ │        │             │ │                          │
>   └───┼→┌──────────────┐   │ │        ▼             │ │ ┌────────────────────┐   │
>       │ │ 🌐 Web App   │───┘ │ ┌────────────────┐   │ │ │ Internal Service B │   │
>       │ └──────────────┘     │ │ ☸ Kubernetes   │   │ │ └────────────────────┘   │
>       │                      │ │ │ Cluster        │───┼─┼──────────────┐           │
>       │                      │ │ └────────────────┘   │ │              │ TCP 5432  │
>       ╰──────────────────────╯ ╰──────────────────────╯ │              ▼           │
>                                                       │ ┌────────────────────┐    │
>                                                       │ │ 🗄 PostgreSQL       │    │
>                                                       │ │ 198.x.x.x :5432    │    │
>                                                       │ └────────────────────┘    │
>                                                       ╰──────────────────────────╯
> ```
>
> Treat the reference image as the **topology/layout reference**, but substantially improve the frontend visual quality.
>
> The goal is a component that looks convincing enough to be used in a real internal infrastructure/network-management application.
>
> After implementation:
>
> 1. run the Angular/TypeScript build,
> 2. fix all compile/type errors,
> 3. check that nodes do not overlap,
> 4. check edge labels don't overlap nodes,
> 5. ensure zones remain visually behind their nodes,
> 6. ensure zoom/pan works,
> 7. give me a concise summary of the files created/changed and any assumptions you had to make.

One important part is **“inspect the installed diagram package and do not invent APIs.”** Coding agents have a tendency to recognize “ngDiagram,” assume a particular library/API, and then generate code that looks plausible but does not compile. This wording forces it to adapt the design to the actual Angular project instead.
