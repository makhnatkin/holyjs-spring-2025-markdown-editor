---
layout: intro
---

### Часть 3
# Архитектура

<!--
(end) ####################################
-->

---
layout: center
subtitle: Архитектура
---

# WYSIWYG

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# Редакторы первого поколения

* CKEditor (2003);
* TinyMCE (2004).

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
image: /part3/ckeditor.png
subtitle: Архитектура
copyright: "фото – https://stackoverflow.com/questions/26660006"
---

<Mode :wysiwyg="true" />



<!--
(end) ####################################
-->


---
layout: default
image: /part3/tinymce.png
subtitle: Архитектура
copyright: "фото – wordpress.org"
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 3rem
---

<img src="/part3/generation-old.png" />

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# Недостатки редакторов<br>первого поколения

* зависимость от contenteditable и DOM;
* отсутствие структурированной модели данных;
* изначально не рассчитаны на совместное редактирование.

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: center
subtitle: Архитектура
size: 4rem
---

# 10 лет спустя

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# Редакторы с внутренней<br>моделью документа

* Quill (2014);
* ProseMirror (2015);
* Draft.js (2016);
* Slate.js (2017);
* Editor.js (2018);
* CKEditor 5 (2018);
* Lexical (2022).

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 3rem
---

<img src="/part3/generation-new.png" />

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# Почему выбрали ProseMirror?

* гибкость и расширяемость: настраивается через схемы и плагины;
* строгий контроль: схема гарантирует валидность документа;
* совместное редактирование: поддержка через Yjs и встроенные шаги;
* высокая производительность: оптимизация DOM для больших текстов;
* стабильность: неизменяемые структуры данных;
* модульность: разделение модели, состояния и view;
* активное сообщество: Tiptap, Remirror и другие проекты.

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: two-cols
subtitle: Архитектура
---
# ProseMirror vs Draft.js/Editor.js

* Draft.js/Editor.js проще: легче начать, но меньше гибкости;
* ProseMirror по схеме: cтрогая структура vs JSON;
* совместное редактирование: встроено в ProseMirror, нет в других;
* производительность: ProseMirror лучше для больших текстов.

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---


# ProseMirror vs Slate.js

* Slate.js для React, ProseMirror независим от фреймворков;
* ProseMirror по схеме, Slate.js выше риск невалидной структуры;
* производительность: ProseMirror стабильнее на больших объёмах;
* совместное редактирование: встроено в ProseMirror, нет в Slate.js.

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# ProseMirror vs Lexical

* Lexical набирает обороты, ProseMirror зрелый и проверенный;
* схема vs буфер: ProseMirror строже, Lexical гибче;
* DOM-обновление: ProseMirror прямое, Lexical с мини-DOM;
* совместное редактирование: оба поддерживают Yjs.

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Архитектура ProseMirror

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->



---
layout: default
subtitle: Архитектура
image: /part3/legovsmatchbox.png
right: true
---

> The core library is not an easy drop-in component—we are prioritizing modularity and customizability over simplicity, with the hope that, in the future, people will distribute drop-in editors based on ProseMirror. As such, this is more of a Lego set than a Matchbox car.

Marijn Haverbeke

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: two-cols
subtitle: Архитектура
---

# Из чего состоит ProseMirror?

* **prosemirror-model**. Модель документа.<br/>Структура данных для содержимого; 
* **prosemirror-state**. Состояние редактора.<br/>Выделение + транзакции; 
* **prosemirror-view**. Интерфейс редактора.<br/>Отображение + взаимодействие; 
* **prosemirror-transform**. Изменение документа.<br/>Запись, воспроизведение, основа транзакций.

<Mode :wysiwyg="true" />


<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{1,3-16|all}
// 1. schema
import {Schema} from 'prosemirror-model';

const schema = new Schema({
    nodes: {
        // ...
        paragraph: {
            content: 'inline*',
            group: 'block',
            parseDOM: [{tag: 'p'}],
            toDOM() {
                return ['p', 0];
            },
        },
    }
});
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 1rem
---

```ts{1,5-|all}
// 2. parser
import MarkdownIt from 'markdown-it';
import {MarkdownParser} from 'src/core/markdown/MarkdownParser';

const md = new MarkdownIt();
const parser = new MarkdownParser(schema, md, {
        // ...
        paragraph: {
            name: 'paragraph',
            type: 'block',
        },
    },
    {},
);
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 1rem
---

```ts{1,3-|all}
// 3. serializer
import {MarkdownSerializer} from 'src/core/markdown/MarkdownSerializer';

const serializer = new MarkdownSerializer({
        // ...
        paragraph: (state, node) => {
            state.renderInline(node);
            state.closeBlock(node);
        },
    },
);
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 1rem
---

```ts{1,9-|all}
// 4. command
import {
    chainCommands,
    createParagraphNear,
    liftEmptyBlock
} from 'prosemirror-commands';
import type {Command} from 'prosemirror-state';

const enterCmd: Command = chainCommands(
    createParagraphNear,
    liftEmptyBlock,
);
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 1rem
---

```ts{1,6-|all}
// 5. state
import {ellipsis, emDash, inputRules} from 'prosemirror-inputrules';
import {keymap} from 'prosemirror-keymap';
import {EditorState} from 'prosemirror-state';

const initialMarkup = 'Привет, мир!';
const state = EditorState.create({
    schema,
    doc: parser.parse(initialMarkup),
    plugins: [
        keymap({ Enter: enterCmd }),
        inputRules({ rules: [ellipsis, emDash] }),
    ],
});
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 1rem
---

```ts{1,4-|all}
// 6. view
import {EditorView} from 'prosemirror-view';

const view = new EditorView(
    null, 
    { state }
);

const markup = serializer.serialize(view.state.doc);
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Добавили<br />менеджер расширений

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 0.82rem
---

```ts{all|3-8|9-12|13-16|2|all}
const ParagraphExtension: Extension = (builder) => {
    builder.addNode('paragraph', () => ({
        spec: {
            content: 'inline*',
            group: 'block',
            parseDOM: [{tag: 'p'}],
            toDOM() { return ['p', 0]; },
        }, 
        fromMd: {
            tokenName: 'paragraph',
            tokenSpec: {name: 'paragraph', type: 'block'},
        }, 
        toMd: (state, node) => {
            state.renderInline(node);
            state.closeBlock(node);
        },
    }))};
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{all|9|all}
const KeymapExtension: Extension = (builder) => {
    const enterCmd: Command = chainCommands(
        newlineInCode,
        createParagraphNear,
        liftEmptyBlock,
        splitBlock,
    );

    builder.addKeymap(() => ({
        Enter: enterCmd,
    }));
};
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{2|all}
const LinkExtension: Extension = (builder) => {
    builder.addMark('link', () => ({
        spec: {
          // ...
        },
        fromMd: {
          // ...
        },
        toMd: {
          // ...
        },
    }));
};
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{all|8-11|1|14|all}
const editor = new WysiwygEditor({
    initialContent: 'Привет, мир!',
    extensions: (builder) =>
        builder
            // ...
            .use(DocExtension)
            .use(TextExtension)
            .use(ParagraphExtension)
            .use(LinkExtension)
            .use(KeymapExtension)
            .use(InputExtension),
});

const markup = editor.getValue();
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->



---
layout: center
subtitle: Архитектура
---

# Redux -> Redux Toolkit

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 0.75rem
---

```ts{all|1-3|5-8|10-20|all}
// Action Types
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

// Action Creators
export const increment = () => ({ type: INCREMENT });
export const decrement = () => ({ type: DECREMENT });

// Reducer
const initialState = { count: 0 };
export const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case INCREMENT:
      return { ...state, count: state.count + 1 };
    case DECREMENT:
      return { ...state, count: state.count - 1 };
    default:
      return state;
  }
};
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 0.75rem
---

```ts{all|4-9|all}
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { count: 0 },
  reducers: {
    increment: (state) => { state.count += 1; },
    decrement: (state) => { state.count -= 1; }
  }
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Работа по позициям

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
image: /part3/pos-tree.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
image: /part3/pos-pos.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
image: /part3/pos-pos-tree.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
image: /part3/pos-pos-devtools.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Тримминг списка

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
image: /part3/list-initial.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
image: /part3/list-copy.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
image: /part3/list-empty.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
image: /part3/list-paste.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
image: /part3/list-devtools-tree.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
image: /part3/list-devtools-pos.png
---

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{all}
type Poses = [number, number, number, number];
export function findNotEmptyContentPosses(fragment: Fragment): Poses {
    let firstNodePos = -1;
    let lastNodePos = -1;
    let firstNotEmptyNodePos = -1;
    let lastNotEmptyNodePos = -1;

    fragment.forEach((contentNode, offset) => {
        // ...
        lastNodePos = offset + contentNode.nodeSize;
        if (!isEmptyString(contentNode)) {
            // манипуляции с позициями
        }
    });

    return [firstNotEmptyNodePos, lastNotEmptyNodePos, firstNodePos, lastNodePos];
}
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{all}
// манипуляции с позициями
if (isListNode(contentNode) || isListItemNode(contentNode)) {
    const [start, end] = findNotEmptyContentPosses(contentNode.content);
    if (firstNotEmptyNodePos === -1 && start !== -1) {
        firstNotEmptyNodePos = offset + start;
    }
    if (end !== -1) {
        lastNotEmptyNodePos = offset + end;
    }
} else {
    if (firstNotEmptyNodePos === -1) {
        firstNotEmptyNodePos = offset;
    }
    lastNotEmptyNodePos = offset + contentNode.nodeSize;
}
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 0.9rem
---

```ts{all|10|all}
export function trimContent(
    fragment: Fragment,
    creatEmptyFragment?: () => Fragment
): Fragment {
    const [
        notEmptyStart, notEmptyEnd, start, end
    ] = findNotEmptyContentPosses(fragment);

    // ...
    return fragment.cut(notEmptyStart + 1, notEmptyEnd + 1);
}
```

<Mode :wysiwyg="true" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Расширения<br/>в режиме разметки

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->



---
layout: default
image: /part3/how-to-create.png
subtitle: Архитектура
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Стандарт<br />директивного синтаксиса

<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->


---
layout: default
image: /part3/commonmark-directives.png
subtitle: Архитектура
---

<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->

---
layout: default
subtitle: Архитектура
codeSize: 1.2rem
---

```md{all|1,2|4,5|7-10|all}
# 1. Inline Directive Syntax
:name[content]{key=val}

# 2. Leaf Block Directives
:: name [content] {key=val}

# 3. Container Block Directives
::: name [inline-content] {key=val}
contents, which are sometimes further block elements
:::
```

<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->


---
layout: default
image: /part3/directives.png
subtitle: Архитектура
---


<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->


---
layout: default
subtitle: Архитектура
codeSize: 1.4rem
---

```md{all|3,6|4-5|all}
## Это заголовок, а ниже разметка HTML блока

::: html
  <h1>Красивый заголовок первого уровня</h1>
  <p>Вдохновляющий текст</p>
:::
```


<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->


---
layout: default
image: /part3/commonmark-directives-ready.png
subtitle: Архитектура
---

<Mode :wysiwyg="false" />

<!--
(end) ####################################
-->


---
layout: center
subtitle: Архитектура
---

# Почему выбрали CodeMirror?

<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->





---
layout: two-cols
subtitle: Архитектура
---

# Monaco vs CodeMirror

* Monaco мощный: тяжёлый, с функциями IDE;
* CodeMirror лёгкий: гибкий и компактный;
* ProseMirror и CodeMirror один автор (Marijn Haverbeke).

<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->

---
layout: two-cols
subtitle: Архитектура
---

# Возможности CodeMirror

* лёгкость и компактность: минимальный вес, быстрая загрузка;
* гибкая кастомизация: темы и плагины под любые задачи;
* подсветка синтаксиса: быстрая работа со множеством языков;
* автодополнение: умные подсказки в реальном времени;
* виртуализация: эффективная работа с большими файлами;
* модульность: подключение только нужных функций;
* активное сообщество: регулярные обновления и плагины.


<Mode :wysiwyg="false" />


<!--
(end) ####################################
-->
