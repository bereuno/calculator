# Super Calculator

## Project overview

An Angular calculator built for teaching purposes. It targets students learning
Angular fundamentals (standalone components, property/event binding, unit
testing with Karma + Jasmine) through a small, self-contained UI project.

## Tech stack

- Angular 19.2 (standalone components, no NgModules)
- TypeScript 5.7 with strict compiler options (`strict`, `noImplicitOverride`,
  `noPropertyAccessFromIndexSignature`, `noImplicitReturns`,
  `noFallthroughCasesInSwitch`)
- RxJS + zone.js (Angular's default change-detection stack)
- Karma + Jasmine for unit tests, run in Chrome/ChromeHeadless

## How to run

- Install: `npm install`
- Dev server: `npm start` → http://localhost:4200 (auto-reloads on save)
- Tests: `npm test` (interactive, watches for changes)
  - Headless/CI run: `npx ng test --watch=false --browsers=ChromeHeadless`
- Build: `npm run build` → output in `dist/`

## Project structure

- `src/app/app.component.ts` — all calculator logic and state (display,
  operands, operator, theme flag) lives in this single root component
- `src/app/app.component.html` — template; wires buttons to component methods
  via event binding and conditionally applies the `light` theme class
- `src/app/app.component.css` — component-scoped styles, including the
  dark (default) and light theme rules
- `src/app/app.component.spec.ts` — full unit test suite for the component
- `src/app/app.config.ts` — application-level providers/bootstrap config
- `src/main.ts` — application entry point

## Exercises

`requirements.md` originally defined three parts of student exercises. All
three are now complete:

1. **`pressToggleSign()` / `pressPercent()`** — implemented in
   `app.component.ts` (sign flip with `-0` guard, divide-by-100 conversion).
2. **Unit tests** — all `pending()` placeholders in `app.component.spec.ts`
   have been replaced with real assertions (multi-digit input, decimal point
   handling, clear cancelling a pending operation, subtraction, multiplication,
   decimal division, chained operations, toggle-sign, and percent).
3. **`toggleTheme()` + light-mode CSS** — implemented, including a
   `@HostBinding('class.light')` on `isLightMode` so the `:host.light` rule
   in `app.component.css` actually applies to the page background (the
   template only bound the `light` class to the `.calculator` div).

The `karma`, `karma-jasmine`, `karma-chrome-launcher`,
`karma-jasmine-html-reporter`, `karma-coverage`, and `jasmine-core`
dev dependencies were also added to `package.json`, since `karma.conf.js`
referenced them but they were missing, which made `npm test` fail.

There are no open exercises left; treat this as a finished reference
implementation rather than a partially-built starter.

## Coding conventions

- Public methods have a JSDoc comment explaining what they do and, for
  non-obvious cases, why (e.g. the `-0` edge case in `pressToggleSign`)
- Related members are grouped under banner comments, e.g.
  `// ─── State ────...────` and `// ─── Button handlers ────...────`
- Method names are camelCase and describe the user action they handle
  (`press*` for button presses, `toggle*` for on/off switches)
- No abbreviations in identifiers; prefer full words (`firstOperand`, not `op1`)
