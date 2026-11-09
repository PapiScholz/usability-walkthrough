# Measuring a screen

Run inside the page (e.g. Playwright `page.evaluate`) after the main heading is visible. Measure load time with a timer around navigation *inside one script*, never across two tool calls.

```js
() => {
  const vis = (e) => { const b = e.getBoundingClientRect(); return b.width > 0 && b.height > 0; };
  const controls = [...document.querySelectorAll('main button, main a, main input:not([type=checkbox]):not([type=radio]), main select, main [role=tab]')].filter(vis);
  const small = controls.filter((e) => e.getBoundingClientRect().height < 40)
    .map((e) => (e.innerText || e.getAttribute('aria-label') || e.placeholder || e.tagName).trim().slice(0, 30));
  const disabledNoReason = [...document.querySelectorAll('main button:disabled')].filter(vis)
    .filter((b) => !b.title && !b.getAttribute('aria-describedby')).map((b) => b.innerText.trim().slice(0, 30));
  return {
    controls: controls.length,
    under40px: small.length, examples: [...new Set(small)].slice(0, 6),
    disabledNoReason,
    horizontalOverflow: document.documentElement.scrollWidth > window.innerWidth,
    pageHeight: document.documentElement.scrollHeight,
  };
}
```

Also, once per project:
- `grep -rnE "\b(alert|confirm|prompt)\(" <src>` — native dialogs. Leads only: check which ones sit on frequent paths.
- Console errors during the walkthrough: explain each one (expected 4xx from a provoked trap is fine; say so).
- Very tall pages (>3 screens) with many controls usually mean a settings page that needs sections.
