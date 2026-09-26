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

**A. FINAL TEAM STRUCTURE**

**ABHIMANTHA** — **Technical Architecture & Algorithms Lead**  
Primary technical decision-maker.  
Owns system architecture, GIS strategy, routing/optimization algorithms, frontend/product implementation, integration, deployment, debugging, technical feasibility, and final technical scope.

**YUMETH** — **Software & Data Pipeline Lead**  
Owns NASA/partner data ingestion, preprocessing, backend services, data contracts, caching, raster-processing utilities, automated tests, reproducibility, error handling, and technical data validation.  
Works from agreed scientific and architectural contracts.

**ISATH** — **Planetary Science & Product Research Lead**  
Owns challenge interpretation, planetary-science research, dataset scientific meaning, mission/user research, assumptions, feature-value analysis, scientific interpretation, limitations, and presentation content. Provides scientific review of technical decisions but does not own system architecture or GIS implementation unless demonstrated capability changes.

**THUSAL** — **Science Research & Validation Lead**  
Owns technical literature research, mission/environment context, source verification, assumptions tracking, manual validation examples, fact-checking, judge questions, and scientific communication.

**Main Overlaps**

**Abhimantha ↔ Yumeth**

* both touch backend/integration  
* both touch technical validation  
* both may naturally end up debugging shared problems

**Boundary:**  
Abhimantha owns **architecture, interfaces, algorithms, integration and technical scope**.  
Yumeth owns **implementation of the data/backend pipeline inside those interfaces**.

Abhimantha should not become the person who writes every service because nobody else knows how it works.

**Isath ↔ Thusal**

* both conduct scientific research  
* both evaluate scientific claims  
* both communicate scientific findings

**Boundary:**  
Isath owns **scientific interpretation and product meaning**.  
Thusal owns **verification and evidence integrity**.

A convenient distinction:

> **Isath asks:** “What does this mean for the project?”  
> **Thusal asks:** “Can we actually prove that?”

This preserves the scientific-review model already specified in the source.

| Person | Primary Role | Owns | Reviews | Does Not Own |
| :---: | ----- | ----- | ----- | ----- |
| **Abhimantha** | Technical Architecture & Algorithms Lead | Architecture, algorithms, routing strategy, frontend implementation, integration, deployment, technical feasibility, final technical scope | Backend/data implementation, scientific/product feasibility | Every backend task, routine data processing, primary scientific claims |
| **Yumeth** | Software & Data Pipeline Lead | Ingestion, preprocessing, backend services, data contracts implementation, caching, technical QA, automated testing, reproducibility | Architecture implementation feasibility, data-related technical decisions | System architecture, product scope, scientific meaning, routing design |
| **Isath** | Planetary Science & Product Research Lead | Challenge interpretation, scientific interpretation, NASA dataset evaluation, product workflow, UX reasoning, research synthesis, presentation narrative, control-document stewardship | Scientific assumptions, product scope, presentation/demo story | System architecture, GIS implementation, backend architecture, routing algorithms |
| **Thusal** | Science Research & Validation Lead | Evidence verification, citations, assumption verification, scientific validation evidence, manual scientific tests, source integrity, judge-question evidence | Scientific research, claims, limitations, research conclusions | Architecture, backend, product scope, unsourced scientific decisions |

