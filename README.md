# shtml-modules
Server-side renderer of html modules

https://github.com/WICG/webcomponents/blob/gh-pages/proposals/html-modules-explainer.md

```html
<template id="myCustomElementTemplate">
    <div>Custom element shadow tree content...</div>
</template>

<script type="module">
    let importDoc = import.meta.document;

    class myCustomElement extends HTMLElement {
        constructor() {
            super();
            let shadowRoot = this.attachShadow({ mode: "open" });
            let template = importDoc.getElementById("myCustomElementTemplate");
            shadowRoot.appendChild(template.content.cloneNode(true));
        }
    }

    window.customElements.define("myCustomElement", myCustomElement);
</script>

<script type=ssr>
</script>
```

Establish sla.  Say maximum time to render cannot exceed 0.2 seconds.

Can plug in server-side renderers of certain combinations of components.

For example

```html
<xtal-fetch href="https://mydomain/api/" ss-file-path="//sans-share/guid/myJson.json"></xtal-fetch>
<p-d val-from-target=value to [-list]></p-d>
<repeat-er -list render-to=ul>
    <template><li>{{displayText}}</li></template>
</repeat-er>
<ul>
</ul>
```

Server side attempts to retrieve json.  If it can do it before 0.2 seconds runs out, generates the same html the other 3 tags would produce.

If not, optionally updates the href maybe with a key it knows will have the data when it's available (since the data is already being retrieved, maybe it could be placed in redis cache or something really fast once obtained). 
