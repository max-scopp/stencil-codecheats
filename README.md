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

[Mark](https://github.com/marksyzm) wrote an HTML exposer.
Not sure for what it's maybe needed, but it looks like an valuable snippet.

```typescript
import { Component, Element } from '@stencil/core';

@Component({
  tag: 'html-exposer',
  styleUrl: 'html-exposer.css',
  shadow: true
})
export class HtmlExposer {
  @Element() private _hostEl: HTMLElement;

  appendSlotContentToDOM (el: HTMLElement) {
	if (!this._hostEl.contains(el)) {
		this._hostEl.appendChild(el);
	}
  }

  public render() {
    return (
      <slot name="exposeslot">
        <div slot="exposeslot" ref={this.appendSlotContentToDOM.bind(this)}>
            Hi there! You can see me in the real DOM!
        </div>
      </slot>
    );
  }
}
```
