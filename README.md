**PERIAPSIS**  
**Team Operating System**

**NASA International Space Apps Challenge 2026 — Colombo**  
**Working Challenge:** *Interplanetary Survival Guide: Martian Map*  
**Operating period:** 19 September – 28 October 2026  
**Major reset point:** 28 October 2026

**Operating principle:** Working \> reliable \> understandable \> impressive \> elegant.

**ABOUT THE CHALLENGE**

NASA has explored Mars robotically for decades, studying its extreme environment, mapping its surface, and collecting many types of data. Far from home, the first astronauts to set foot on Mars will want the best map possible, with information on the details of their routes and destinations, updates on current conditions, and the data needed to complete their mission quickly and safely. Your challenge is to create a layered, integrated view of a location or route on the Martian surface that pulls together data from multiple NASA science missions and could help a human explorer plan and carry out a successful Marswalk while conducting new and exciting science along the way.

---

**A. CURRENT TEAM STRUCTURE (as of 13 October 2026)**

**ABHIMANTHA** — **Technical Architecture & Algorithms Lead**  
Primary technical decision-maker.  
Owns system architecture, GIS strategy, routing/optimization algorithms, frontend/product implementation, integration, deployment, debugging, technical feasibility, and final technical scope.

**YUMETH** — **Software & Data Pipeline Lead**  
Owns NASA/partner data ingestion, preprocessing, backend services, data contracts, caching, raster-processing utilities, automated tests, reproducibility, error handling, and technical data validation.  
Works from agreed scientific and architectural contracts.

**ISATH** — **Planetary Science & Product Research Lead**  
Owns challenge interpretation, planetary-science research, dataset scientific meaning, mission/user research, assumptions, feature-value analysis, scientific interpretation, limitations, and presentation content. Provides scientific review of technical decisions but does not own system architecture or GIS implementation unless demonstrated capability changes.

**SENULA** — **Terrain & Routing Implementation Engineer (proposed assignment)**  
Proposed focus: implementing terrain-cost and route-planning modules, graph search, route metrics, unit tests, and reproducible validation examples within the agreed interfaces. Abhimantha retains algorithm/architecture ownership; Yumeth provides validated terrain inputs; Isath reviews scientific assumptions. Senula's exact scope remains provisional until reviewed against a working trial and integration requirements.

**Main Overlaps**

**Abhimantha ↔ Yumeth**

* both touch backend/integration  
* both touch technical validation  
* both may naturally end up debugging shared problems

**Boundary:**  
Abhimantha owns **architecture, interfaces, algorithms, integration and technical scope**.  
Yumeth owns **implementation of the data/backend pipeline inside those interfaces**.

Abhimantha should not become the person who writes every service because nobody else knows how it works.

**Abhimantha ↔ Senula**

* both work on terrain-aware routing
* both may test and debug route calculations

**Boundary:**  
Abhimantha owns the routing strategy, cost-model specification, algorithms at the design level, API contract, integration, and final technical scope.  
Senula is the proposed implementer of defined terrain/routing modules and their tests. Scientific assumptions and parameter changes require Isath's review.

**Yumeth ↔ Senula**

* both handle raster-derived terrain data
* both validate intermediate values

**Boundary:**  
Yumeth owns NASA data ingestion, metadata, reprojection/preprocessing, and standardized raster outputs.  
Senula consumes the agreed terrain data interface to implement route costs and paths; he does not independently redefine upstream data contracts.

**Scientific evidence and review**

Isath owns the source/evidence register, interpretation, limitations, and presentation claims. Yumeth independently checks data provenance, units, metadata, and transformations. Senula checks representative terrain and routing examples within his assigned scope. Abhimantha checks that the final product/demo claims match the implementation.

**Rule:** Every consequential scientific claim needs a traceable source or documented calculation and a second-person review. Scientific verification needs an explicit owner and reviewer.

| Person | Primary Role | Owns | Reviews | Does Not Own |
| :---: | ----- | ----- | ----- | ----- |
| **Abhimantha** | Technical Architecture & Algorithms Lead | Architecture, algorithms, routing strategy, frontend implementation, integration, deployment, technical feasibility, final technical scope | Backend/data implementation, scientific/product feasibility | Every backend task, routine data processing, primary scientific claims |
| **Yumeth** | Software & Data Pipeline Lead | Ingestion, preprocessing, backend services, data contracts implementation, caching, technical QA, automated testing, reproducibility | Architecture implementation feasibility, data-related technical decisions | System architecture, product scope, scientific meaning, routing design |
| **Isath** | Planetary Science & Product Research Lead | Challenge interpretation, NASA dataset scientific meaning, mission/user research, product workflow, evidence register, limitations, presentation narrative, control-document stewardship | Scientific assumptions, product scope, presentation/demo story | System architecture, GIS implementation, backend architecture, routing algorithms |
| **Senula** | Terrain & Routing Implementation Engineer (proposed) | Defined terrain-cost/routing modules, route metrics, algorithm test cases and integration fixtures, subject to trial review | Route behaviour, terrain constraints, manual path calculations | System architecture, backend/data ingestion, independent scientific or routing-scope changes |

