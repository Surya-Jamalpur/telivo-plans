# Telivo plan catalog

Public recharge-plan data downloaded by the Telivo app, so plan prices can
change without an app release. Contains only public plan prices — no code,
no user data.

**Do not edit `plan-catalog.json` by hand.** It is generated in the app repo:

1. Edit `src/data/plans/<operator>-prepaid.json` in the Telivo app repo.
2. Bump that file's `updatedAt` (e.g. `2026-10-21`, or `2026-10-21T18:30`
   for a second change on the same day). Phones only accept a newer
   `updatedAt`, so an older file can never roll prices back.
3. Run `npm run build:plans -- ../telivo-plans/plan-catalog.json`.
4. Commit and push this repo. Phones pick it up within ~12 hours, or when
   the user taps refresh on the dashboard. GitHub can take up to ~5 minutes
   to serve a just-pushed change.

The app validates the file before using it: a broken or partial file is
ignored and users keep their current plans.
