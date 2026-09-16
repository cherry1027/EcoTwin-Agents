# EcoTwin Agents — Agentic Digital Twin for Energy-Efficient SDVs

EcoTwin Agents is a frontend-only research prototype for exploring how a coordinated set of software agents could reason over a synthetic electric-vehicle digital twin. It is designed as an interactive concept demonstrator, not as a vehicle controller or engineering-validation environment.

> **Research Prototype — Synthetic Vehicle Data & Modeled Energy Effects**

The prototype does not use real RISE data, connect to a real vehicle, implement validated battery physics, claim actual energy savings, or perform production autonomous control.

## Run locally

```bash
npm install
npm run dev
```

Open the local URL printed by the development server. A production build can be checked with `npm run build`.

## Concepts represented

### Software-defined vehicles

A software-defined vehicle (SDV) moves a growing share of vehicle behavior, configuration, diagnostics, and user experience into software. This makes it possible to evolve functions over time, but also raises difficult questions about safety boundaries, update governance, explainability, security, and the division of responsibility between onboard and external systems.

### Digital twins and agentic twins

A digital twin is a computational representation of a physical system that is synchronized with observations and used for monitoring, analysis, or simulation. In this prototype, the twin contains deterministic synthetic state for SOC, battery temperature, speed, consumption, range, HVAC load, traffic, road gradient, outside temperature, and driving style.

An **agentic twin** adds bounded decision-making components around the model. Specialist agents interpret different slices of state, a coordinator reconciles their proposals, the twin simulates modeled effects, and a human reviewer retains final authority for sensitive actions.

### Agency placement

- **External agency** places most reasoning in cloud or fleet services. It can use broader context and larger compute resources, but depends more heavily on connectivity and external data handling.
- **Internal agency** keeps reasoning inside the vehicle. It offers low latency, offline resilience, and stronger data locality, while operating within embedded compute and local-information limits.
- **Distributed agency** divides work among vehicle, edge, cloud, and fleet agents. It can combine local safety constraints with broader optimization context, at the cost of coordination and assurance complexity.

The architecture tab presents these as conceptual trade-offs. The scores are illustrative rather than measured benchmarks.

### Multi-agent coordination

The control room represents six roles: Battery, Driving, Route, Charging, Environment, and Coordinator Agents. Each specialist contributes scoped evidence. The Coordinator Agent combines those signals into deterministic recommendations and exposes the evidence chain rather than presenting a single opaque answer.

The browser experience uses a fixed scenario seed (`ECO-2407`) and deterministic formulas. Repeating a scenario produces the same modeled output.

### Human-in-the-loop governance

The review queue treats agents as advisory components. Each proposal includes its evidence, modeled impact, confidence, affected systems, and risk level. Reviewers can simulate, approve, modify, or reject a proposal. Safety-sensitive recommendations require simulation before approval, demonstrating how policy gates can constrain agent authority.

### Energy optimization

The simulator explores combinations of driving, charging, routing, and distributed coordination. It compares them against a baseline using modeled kWh/100 km, range, battery utilization, charging events, agent agreement, and human overrides. These outputs are useful for interface research and hypothesis formation, not for predicting real vehicle performance.

## Evaluation metrics

- **Energy demand:** synthetic kWh/100 km under the selected scenario.
- **Estimated range:** a simplified function of usable synthetic battery capacity, SOC, and modeled demand.
- **Battery utilization:** a synthetic score representing how effectively the duty cycle uses the modeled pack window.
- **Charging events:** modeled stops over a fixed 240 km duty cycle.
- **Agent agreement:** the proportion of specialist recommendations aligned with the coordinated strategy.
- **Human overrides:** reviewer interventions recorded in the modeled scenario.
- **Confidence:** a fixed, illustrative agent confidence value; it is not calibrated probability.

## Limitations

- All data is deterministic and synthetic; there is no backend, database, login, telemetry stream, or paid API.
- Vehicle and battery relationships are intentionally simplified and are not validated physics models.
- Latency, privacy, compute, connectivity, and complexity scores are conceptual comparisons.
- Range and energy effects omit many real influences, including pack aging, wind, tire state, payload, road surface, cell chemistry, thermal transients, and driver adaptation.
- Agent findings are deterministic interface demonstrations rather than learned or validated control policies.
- Human approval interactions are held in in-memory frontend state and do not constitute a compliant audit record.
- The prototype must not be used for vehicle control, safety decisions, charging operations, or claims about actual savings.

## Stack

React, TypeScript, Vinext/Vite, Tailwind CSS, Radix-based interface primitives, and Lucide icons. The project is frontend-only.
