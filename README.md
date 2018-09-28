# stencil-codecheats
Code Snippets I found to write better code than if you do it from scratch yourself.
Feel free to submit something if it's good practice!

---

### Check for used `<slot/>`s.

```typescript
componentWillLoad() {
  const host = this.el.shadowRoot
  host.addEventListener('slotchange', e => {
    const slot = e.target as HTMLSlotElement
    this.hasDescription = slot.name === 'description' && slot.assignedNodes().length > 0
  });
}
```

Don't accept the gullible way:

```typescript
componentDidLoad() {
  const hasBefore = this._host.querySelector('[slot="before"]') != null;
}
```

---
