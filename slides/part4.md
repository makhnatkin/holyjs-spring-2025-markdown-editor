---
layout: intro
---

### Часть 4
# Вызовы

<!--
(end) ####################################
-->

---
layout: center
subtitle: Вызовы
---

# Случай со списками

<!--
(end) ####################################
-->


---
layout: default
image: /part4/list-p.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/list-wysiwyg.png
subtitle: Вызовы
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: center
subtitle: Вызовы
---

# Где источник истины?


<!--
(end) ####################################
-->

---
layout: default
image: /part4/matrix-pills.jpg
subtitle: Вызовы
copyright: "фото – «Матрица», 1999"
---

<!--
(end) ####################################
-->

---
layout: default
image: /part4/matrix-pills-bw.jpg
subtitle: Вызовы
copyright: "фото – «Матрица», 1999"
---

<!--
(end) ####################################
-->

---
layout: default
image: /part4/list-pr.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/list-li.png
subtitle: Вызовы
---

<!--
(end) ####################################
-->

---
layout: center
subtitle: Вызовы
---


# Модификация разметки

<!--
(end) ####################################
-->


---
layout: default
subtitle: Вызовы
codeSize: 1.1rem
---

```md{all}
### Simple table

#|
|| **Header1** ||
|| Text        ||
|#
```

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/table-wysiwyg.png
subtitle: Вызовы
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/parsing-serialization-table.png
subtitle: Вызовы
---

<!--
(end) ####################################
-->

---
layout: default
subtitle: Вызовы
codeSize: 0.9rem
---

```ts{all|8-9,12|all}
// src/extensions/yfm/YfmTable/YfmTableSpecs

builder.addNode(YfmTableNode.Row, () => ({
    // spec: ...,
    // fromMd: {tokenSpec: ...},
    toMd: (state, node) => {
        state.write('||');
        state.ensureNewLine();
        state.write('\n');
        state.renderContent(node);
        state.write('||');
        state.ensureNewLine();
    },
}))
```

<!--
(end) ####################################
-->

---
layout: default
subtitle: Вызовы
codeSize: 1rem
---

```md{all}
### Simple table

#|
||

**Header1**

||
||

Text

||
|#
```

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/parsing-serialization-dyn.png
subtitle: Вызовы
---

<!--
(end) ####################################
-->


---
layout: default
subtitle: Вызовы
codeSize: 0.9rem
---

```ts{all|9|10|12|13|all}
/**
 * - Assigns a unique `data-token-id` to each token.
 * - Captures and stores the raw Markdown using `MarkupManager`.
 */
process: (token, _, rawMarkup) => {
    const {map} = token;

    if (map) {
        const content = rawMarkup.split('\n').slice(map[0], map[1]).join('\n');
        const tokenId = v5(content, markupManager.getNamespace());

        token.attrSet(YFM_TABLE_TOKEN_ATTR, tokenId);
        markupManager.setMarkup(tokenId, content);
    }
    return token;
},
```

<!--
(end) ####################################
-->

---
layout: default
subtitle: Вызовы
codeSize: 0.9rem
---

```ts{all|6|all}
/**
 * - Links the token to its corresponding node via `data-node-id`.
 */
process: (token, attrs) => ({
    ...attrs,
    [YFM_TABLE_NODE_ATTR]: token.attrGet(YFM_TABLE_TOKEN_ATTR),
}),
```

<!--
(end) ####################################
-->

---
layout: default
subtitle: Вызовы
codeSize: 0.9rem
---

```ts{all|11|12|all}
/**
 * - Retrieves the original Markdown using the `data-node-id` attribute.
 * - Uses the original Markdown if the node matches the saved version.
 * - Falls back to schema-based rendering if the node structure, attributes,
 *   or parent elements affect it.
 */
process: (state, node, parent, index, callback) => {
    const nodeId = node.attrs[YFM_TABLE_NODE_ATTR];
    const savedNode = markupManager.getNode(nodeId);

    if (!PARENTS_WITH_AFFECT.includes(parent?.type?.name) && savedNode?.eq(node)) {
        state.write(markupManager.getMarkup(nodeId) + '\n');
        return;
    }
    callback?.(state, node, parent, index);
},
```

<!--
(end) ####################################
-->

---
layout: center
subtitle: Вызовы
---

# Что является контентом?

<!--
(end) ####################################
-->


---
layout: default
image: /part4/content-text.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/content-break.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->

---
layout: default
image: /part4/content-space.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->


---
layout: default
image: /part4/content-break.png
subtitle: Вызовы
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->
