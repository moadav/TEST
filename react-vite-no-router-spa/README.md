# Mutator acceptance fixture: react-vite-no-router-spa

The first milestone from the test plan: routerless React/Vite SPA, no head wiring.

- `repo/`   — baseline. A real, building Vite SPA. Detector: **Partial / Eligible**
              (global title in index.html, no per-route mechanism). Verified: `npm install`,
              `tsc --noEmit`, `vite build` all pass.
- `golden/` — the hand-written target end-state the mutator must reproduce: `react-helmet-async`
              added, **exactly one** `<HelmetProvider>` mounted in `main.tsx`, one `<Helmet>` with a
              static title + description in `App.tsx`. Verified: install + tsc + vite build all pass.
              Detector on this tree: **Ready / NotEligible**.
- `expected.json` — what the acceptance harness asserts.

The harness does NOT diff against `golden/` — `golden/` is a reference and a proof that the recipe
compiles. The harness runs the real gate: mutate a throwaway copy of `repo/`, install + build, re-run
the detector, and require Ready + no duplicate provider. Build green + detector Ready is the pass,
however the mutator chooses to get there.
