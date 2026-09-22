
## Toy example: glacier mass-balance reconciliation

The worked example used to reason about what this harness should enable:
reconciling glacier mass-balance estimates across satellite altimetry,
GRACE/GRACE-FO gravimetry, geodetic DEM differencing, and regional models —
currently a slow, largely manual, multi-year community effort. A working
harness would:

- Encode domain conventions as skills (density assumptions for ice/firn/snow,
  reference-frame reconciliation between methods, debris-cover corrections).
- Use hooks to catch known failure modes mechanically (unit/sign errors,
  cloud-contaminated pixels misread as melt) before they reach a human.
- Use a Ralph loop to process large glacier inventories across many short
  passes rather than one long session.
- Enforce the generator/evaluator split so no reconciled estimate ships
  without independent verification.
- Produce versioned, reproducible output ("harness v2.3, skill pack commit X,
  verified by hooks Y") so results can be regenerated and checked years later.

The goal: turn reconciliation from an occasional landmark community effort
into a continuous, auditable process — freeing domain scientists to focus on
interpreting physical processes rather than re-doing method reconciliation by
hand.