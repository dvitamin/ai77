# Accessibility

Cross-cutting requirements that apply to every view and visualization, not
just the ones that exist when this was written.

## Text contrast

- All text **must** meet WCAG AA contrast against its background: 4.5:1
  for normal text, 3:1 for large text (roughly 18pt+, or 14pt+ bold).
- Text **must not** sit directly over a chart area or image where the
  background varies. Put it on a solid background instead.

## Color in visualizations

- Color **must not** be the only way information is conveyed. Any
  distinction made by color (e.g. abnormal vs. normal lab values) also
  needs a second cue: a label, shape, pattern or position.
- Palettes **must** stay distinguishable for the common forms of color
  vision deficiency.
- Meeting these requirements and looking good are the same goal. Pick a
  palette that does both instead of one that only passes when checked.

## Readability

- Every chart **must** have a text equivalent (e.g. a table or summary)
  for screen readers, keyboard users and people who prefer exact values.
- Dates, units and reference ranges **must** be shown wherever a value is
  shown, so a value is never ambiguous.

## Keyboard navigation

- Everything a user can do with a pointer **must** also be possible with
  the keyboard alone: reaching each chart, switching views, changing what
  a chart shows (e.g. its time range), and opening and closing details.
- The element that has keyboard focus **must** be clearly visible.
- Focus order **must** follow the visual reading order.
- Stepping between individual data points inside a chart with the
  keyboard is **not** required. The chart's text equivalent gives keyboard
  users the exact values instead.

## Open questions

- None right now.
