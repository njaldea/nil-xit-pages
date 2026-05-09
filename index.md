A lightweight distributed reactive runtime for shared state synchronization, live instrumentation, and multi-client visualization.

---

## Core idea

nil-xit separates **execution**, **state**, and **frontend rendering**.

- The `nil-xit` runtime owns frame semantics, lifecycle, and message handling. Execution is expressed as frame logic; transport is delegated to `nil-service`.
- Frontends are **ephemeral sessions**
This enables live shared visualization of running systems, tests, and experiments without embedding a UI framework into the host application.

---

## System model

- frontend (projection layer)
  - stateless
  - emits signals
  - renders values

- nil-service (transport dependency)
  - event loop
  - message forwarding
  - multiplexing clients
  - no semantic awareness

- nil-xit (runtime kernel)
  - owns frames
  - owns semantics
  - owns handlers
  - owns state model

## Frames (primary runtime unit)

Frames are stateful runtime objects and the only distributed unit in nil-xit.

A Frame encapsulates:
- Signals (event definitions)
- Values (reactive state objects)

### Frame primitives

Signals are internal event channels.

Values are externally accessible reactive state objects exposed via handles.

---

## Runtime Flow

![image](https://www.plantuml.com/plantuml/dsvg/VP7DQXin4CVlUeh1bzeKG-DZ3YLkQ4fl8MbBhwfsR8jgHq8pYcDAtxqZMJPhJ7DQq6_c_p5xnsApb34Omxyz9Plj2C4JoY4Xn2oxE06yiqFSUzh2nWR62ScnqE1Y9inmyy4OyH8Go8VbgnV8XSIF29iGzyPaT69fgtpsdNN-ELc7C_XZ05mSKoGaWTawfU2T5Hzf1fPX_VXe_buityUCyDIahzTFrlDVnOS1ywA9_FpwxNBiGSCZVCasxTh0mzErZ6PyyGvXtciSfPv_t5_cKQr8WZJmLPWJWVNHvFFDV_YdpbTL-XqibqiT8vPSN3q4f9rbhCz6pw7VZxKHtCA06qy8czg6ZRvLfcKKjVwmhGtFIvfTYSje1U4zx7r6wELEjbODNzhrcrtTE4jsrlswTj-R_cg6EGlQuG0iEhveIbf-ae7zbcpGGLyF80l5gxVmEKYLkUq1IXfKdYTiTSKqNjN8AWVuYgwqQY76TD6jiteLFf0pvWvfA6Fu1m00)

1. User constructs `nil-service` (transport backend)
2. User constructs `nil-xit` with `nil-service` injected
3. User defines Frames via `nil-xit`, including their signals and values
4. User starts `nil-service` event loop
5. One or more frontends connect and synchronize state
6. Signals flow into frames from frontends
7. Frame values are synchronized back to all frontends

---

## Key properties

- Backend is the single source of truth
- State is automatically rehydrated on reconnect
- UI frameworks are interchangeable

---

## What you can build

### 🧪 Test instrumentation
Wrap test frameworks (e.g. gtest) so each test emits observable frames for live visualization.

### 📓 Notebook integration
Attach Jupyter notebooks to a running runtime and visualize state in real time.

### 📊 Multi-client dashboards
Multiple independent UIs can observe and interact with the same execution.

---

## Supported languages

- C / C++ (core)
- Python bindings
- Lua (experimental / internal)

Frontend is language-agnostic as long as it can communicate with `nil-service`.

Current reference frontend:
- Svelte

---

## Status

- Actively used in internal systems
- Pre-v1 API (subject to change)
- Frontend ergonomics still evolving

---

## Examples

- [nil-sandbox-py](https://github.com/njaldea/nil-sandbox-py)
  - simple Python sandbox using nil-clix, nil-service and nil-xit
- [nil-xit-gtest](https://github.com/njaldea/nil-xit-gtest-example) (vcpkg)
  - adapter layer of nil-xit to a testing framework
- [nil-xit-gtest](https://github.com/njaldea/ppa) (deb system isntall)
  - adapter layer of nil-xit to a testing framework

---

## Repositories

- [nil-xit](https://github.com/njaldea/nil-xit)
- [nil-service](https://github.com/njaldea/nil-service)
- [nil-xit-test](https://github.com/njaldea/nil-xit-test)

---

## Miscellaneous Repositories

- [ppa](https://github.com/njaldea/ppa/tree/ppa)
  - [page](https://njaldea.github.io/ppa/)
- [vcpkg-ports](https://github.com/njaldea/nil-vcpkg-ports)



