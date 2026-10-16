# Vivacity: from simulation to physical proof

*An edited founder–AI build session for Entrepreneurs First · October 2026*

> **The question behind the work:** What would an execution runtime look like if an AI agent could test actions in a physical world, inspect what actually happened, and learn from failure before acting again?

**About this transcript.** This is a condensed, chronological account of the founder’s requests and the resulting engineering work, not a verbatim chat export. Repeated “continue” prompts, troubleshooting minutiae, private credentials, and payment details have been removed. “Build record” passages summarize documented and tested outcomes rather than impersonating the assistant’s original replies. All measurements below describe specific recorded runs, not general performance guarantees.

---

### 01 / Set the standard

**Founder · edited request**  
Build Vivacity as a real execution runtime: inspect a world, fork alternative futures, simulate consequences, evaluate outcomes, commit a state, and replay what happened. Use MuJoCo for robotic dynamics and SciPy for scientific experiments. Preserve full simulation state. Show failures honestly. Do not hardcode a winning trajectory or substitute a video for a simulation.

**Build record**  
The first backend implemented a shared world and experiment contract with state branching, persistence, replay, background jobs, REST APIs, and WebSocket events. Its initial demonstrations were a Franka Panda reaching task in MuJoCo and a simplified orbital hypothesis comparison in SciPy. The product later narrowed to robotics; the orbital lab is part of the development history, not a current public product claim.

### 02 / Make the evidence inspectable

**Founder · edited request**  
Before connecting a frontend, rerun the tests. Execute real robot trajectories, move the obstacle, verify that old results become stale, fit competing orbital models, exercise HTTP and WebSockets, and hand off the API precisely.

**Build record**  
The backend handoff included an OpenAPI export and frontend documentation. Tests and direct requests covered candidate planning, physics execution, collision and success classification, replay, obstacle invalidation, scientific fits, and WebSocket progress. This established the rule that a green build alone would not count as a working demo.

### 03 / Put the world in the user’s hands

**Founder · edited request**  
The app should not start experimenting on page load. Let a user place an object inside the workcell, change its dimensions, mass, and friction, and ask the robot to find a feasible pick-and-place route. Let them pause and resume the simulation. Keep the simulation view focused on the robot and the object.

**Build record**  
The robotics workspace became a user-directed flow with bounded object placement and condition editing, independent candidate trials, measured outcomes, and replay controls. Robot, world, and task choices became an explicit configuration journey. Unsupported combinations were treated as capability boundaries instead of being presented as working physics. The public product demo video documents one Franka Panda warehouse run: 256 candidates were generated and screened; six underwent integrated MuJoCo execution; the best verified placement in that run had 1.1 mm measured error. That result does not establish a global optimum or hardware performance.

### 04 / Turn a factory run into an experiment

**Founder · edited request**  
Changing production settings must change the simulation. Remove visual objects that do not belong in the cell. Derive equations from measured behavior, format them properly in LaTeX, and show when a model fits poorly. Implement in stages, test each stage, inspect the browser, then proceed.

**Build record**  
The Factory flow now creates a fresh MuJoCo cell when bounded settings change and clears stale analysis. A recorded conveyor run executed 1,050 native MuJoCo steps over 2.100 seconds of simulated time and saved 43 frames. A background worker fitted eight descriptive measurement series from those frames; the carton-height model was explicitly labeled **poor fit**. The interface renders equations with LaTeX/MathML and offers measured-data exports. These fits describe simulated observations; they are not discovered physical laws.

### 05 / Ship, then verify the public boundary

**Founder · edited request**  
Deploy a working URL. Check the real public experience, including errors, mobile layout, streaming, replay, and changed conditions. If an acceptance test fails, it is not done.

**Build record**  
The frontend was deployed at [demo.tryvivacity.com](https://demo.tryvivacity.com/), with the simulation backend on Render. In the final recorded release check, the public Factory page completed a browser-started run, displayed 43 saved frames, and served paginated replay plus matching PDF and ZIP exports. A separate public robotics experiment streamed nine WebSocket events across four branches, including failures and an execution success. Moving the obstacle invalidated the previous result; a new experiment ran and selected a branch. The public browser check recorded zero JavaScript errors and no horizontal overflow at a 375 px viewport.

The final recorded test gate was **297 passed, one Linux-specific skip on Windows**; Linux CI passed **298 backend tests** and four constrained-memory checks. **36 frontend checks**, TypeScript, Vite, and the Vercel production build also passed. These are dated release results, not a claim that future deploys cannot regress.

---

### The honest edge of the demo

Vivacity currently demonstrates bounded simulated workcells, measured robot branches, replay, and descriptive mathematical fitting. It does **not** claim hardware-validated manipulation, universal robot/task compatibility, a 5,000-experiment campaign scheduler, or causal law discovery across runs. The official interactive Desmos embed has not been accepted in a production browser without an authorized commercial key. Render’s current Free instance can sleep and uses ephemeral storage, so uninterrupted uptime and durable cross-deployment history are not guaranteed.

The point of the session is the operating discipline: propose an action, run actual physics, keep the evidence, expose failure, change a condition, and run again.
