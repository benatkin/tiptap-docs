> 🚧 This is a work in progress and contributions are welcome. Read the tiptap [contribution guidelines][@tiptap-contrib]
> and help us shape the documentation.

# Built-in extensions
By default, the editor will only support paragraphs. Other nodes and marks are available as **extensions**. You must 
install `tiptap-extensions` package separately so that you can use basic Nodes, Marks, or Plugins. An extension is
usually tied to a [Command](../commands/basics.md). The official set of commands are part of the 
[`tiptap-commands`][@npmjs-tiptap-commands] package.

## Blockquote
Allows you to use the `<blockquote>` HTML tag in the editor.

#### Options
*None*

#### Default Keybindings
- `Ctrl->`

#### Example
```vue
<template>
  <div>
    <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
      <button type="button" :class="{ 'is-active': isActive.blockquote() }" @click="commands.blockquote">
        Blockquote
      </button>
    </editor-menu-bar>

    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { Blockquote } from 'tiptap-extensions'

export default {
  components: {
    EditorMenuBar,
    EditorContent,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new Blockquote(),
        ],
        content: `
          <blockquote>
            Life is like riding a bycicle. To keep your balance, you must keep moving.
          </blockquote>
          <p>Albert Einstein</p>
        `,
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
```

## Bold
Renders text in **bold** text weight. If you pass `<strong>`, or `<b>` tags, or text with inline `style` attributes setting the `font-weight` CSS rule in the editor's initial content, they will be rendered accordingly.

::: warning Restrictions
The extension will generate the corresponding `<strong>` HTML tags when reading contents of the `Editor` instance. All text marked as bold, regardless of method will be normalized to `<strong>` HTML tags.
:::

#### Options
*None*

#### Default Keybindings
- `Ctrl-b` on Windows/Linux
- `Cmd-b` on macOS

#### Example

```vue
<template>
  <div>
    <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
      <button type="button" :class="{ 'is-active': isActive.bold() }" @click="commands.bold">
        Bold
      </button>
    </editor-menu-bar>

    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { Bold } from 'tiptap-extensions'

export default {
  components: {
    EditorMenuBar,
    EditorContent,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new Bold(),
        ],
        content: `
          <p><strong>This is strong</strong></p>
          <p><b>And this</b></p>
          <p style="font-weight: bold">This as well</p>
          <p style="font-weight: bolder">Oh! and this</p>
          <p style="font-weight: 500">Cool! Right!?</p>
          <p style="font-weight: 999">Up to 999!!!</p>
        `,
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
```

## BulletList
Allows you to use the `<ul>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `ListItem` extension. 
:::

## Code
Allows you to use the `<code>` HTML tag in the editor.

#### Options
*None*

#### Default Keybindings
- `Mod-``

#### Example
```vue
<template>
  <div>
    <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
      <button type="button" :class="{ 'is-active': isActive.code() }" @click="commands.code">
        Code
      </button>
    </editor-menu-bar>

    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { Code } from 'tiptap-extensions'

export default {
  components: {
    EditorMenuBar,
    EditorContent,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new Code(),
        ],
        content: `
          <p>This is some <code>inline code.</code></p>
        `,
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
```

## CodeBlock
Allows you to use the `<pre>` HTML tag in the editor.

## HardBreak
Allows you to use the `<hr>` HTML tag in the editor.

## Heading
Allows you to use the headline HTML tags in the editor.

#### Options
| option | type | default | description |
| ------ | ---- | ---- | ----- |
| levels | Array | [1, 2, 3, 4, 5, 6] | Specifies which headlines are to be supported. |

#### Commands
| command | options | description |
| ------ | ---- | ---------------- |
| heading | level | Creates a heading node. |

#### Default Keybindings
- `Shift-Ctrl-1`: H1
- `Shift-Ctrl-2`: H2
- `Shift-Ctrl-3`: H3
- `Shift-Ctrl-4`: H4
- `Shift-Ctrl-5`: H5
- `Shift-Ctrl-6`: H6

#### Example
```vue
<template>
  <div>
    <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
      <div>
        <button type="button" :class="{ 'is-active': isActive.heading({ level: 1 }) }" @click="commands.heading({ level: 1})">
          H1
        </button>
        <button type="button" :class="{ 'is-active': isActive.heading({ level: 2 }) }" @click="commands.heading({ level: 2 })">
          H2
        </button>
      </div>
    </editor-menu-bar>

    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { Heading } from 'tiptap-extensions'

export default {
  components: {
    EditorMenuBar,
    EditorContent,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new Heading({
            levels: [1, 2],
          }),
        ],
        content: `
          <h1>This is a headline level 1</h1>
          <h2>This is a headline level 2</h2>
          <h3>This headline will be converted to a paragraph, because it's not defined in the levels option.</h3>
        `,
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
```

## History
Enables history support.

#### Commands
| command | options | description |
| ------ | ---- | ---------------- |
| undo | none | Undo the latest change. |
| redo | none | Redo the latest change. |

#### Default Keybindings
- `Mod-z`: Undo
- `Shift-Mod-z`: Redo

#### Example
```vue
<template>
  <div>
    <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
      <div>
        <button type="button" @click="commands.undo">
          Undo
        </button>
        <button type="button" @click="commands.redo">
          Redo
        </button>
      </div>
    </editor-menu-bar>

    <editor-content :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import { History } from 'tiptap-extensions'

export default {
  components: {
    EditorMenuBar,
    EditorContent,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new History(),
        ],
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
```

## Italic
Allows you to use the `<em>` HTML tag in the editor.

## Link
Allows you to use the `<a>` HTML tag in the editor.
  
## ListItem
Allows you to use the `<li>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `BulletList` or `OrderedList` extension. 
:::

## OrderedList
Allows you to use the `<ol>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `ListItem` extension. 
:::

## Table
This enables support for tables in your editor.
Tables can be nested and allow all blocks to be used inside.
Each `<TableCell>` includes a single `<Paragraph>`.

#### Options <Badge text="1.19.3"/>
| option | type | default | description |
| ------ | ---- | ---- | ----- |
| resizable | Boolean | false | Enables the resizing of columns |

#### Default Keybindings
- `Tab` Next Cell
- `Shift-Tab` Previous Cell 

#### Commands
| command | options | description |
| ------ | ---- | ---------------- |
| createTable | ```{ rowsCount, colsCount, withHeaderRow }``` | Returns a table node of a given size. `withHeaderRow` defines whether the first row of the table will be a header row. |
| deleteTable | none | Deletes the complete table which is active |
| addColumnBefore | none | Add a column before the selection. |
| addColumnAfter | none | Add a column after the selection. |
| deleteColumn | none | Removes the selected columns. |
| addRowBefore | none | Add a table row before the selection. |
| addRowAfter | none | Add a table row after the selection. |
| toggleCellMerge | none | See mergeCells and splitCells |
| mergeCells | none | Merge the selected cells into a single cell. Only available when the selected cells' outline forms a rectangle. |
| splitCell | none | Split a selected cell, whose rowspan or colspan is greater than one into smaller cells. |
| toggleHeaderColumn | none | Toggles whether the selected column contains header cells. |
| toggleHeaderRow | none | Toggles whether the selected row contains header cells. |
| toggleHeaderCell | none | Toggles whether the selected column contains header cells. |
| setCellAttr | none | Returns a command that sets the given attribute to the given value, and is only available when the currently selected cell doesn't already have that attribute set to that value. |
| fixTables | none | Inspect all tables in the given state's document and return a transaction that fixes them, if necessary. |

#### Example
::: warning
You have to include all table extensions (`TableHeader`, `TableCell` & `TableRow`)
:::

```vue
  <template>
    <div>
      <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
        <button :class="{ 'is-active': isActive.bold() }" @click="commands.createTable({rowsCount: 3, colsCount: 3, withHeaderRow: false })">
          Create Table
        </button>
      </editor-menu-bar>

      <editor-content :editor="editor" />
    </div>
  </template>
  
  <script>
  import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
  import { Table, TableCell, TableHeader, TableRow } from 'tiptap-extensions'


  export default {
    components: {
        EditorMenuBar,
        EditorContent,
    },
    data() {
      return {
        editor: new Editor({
          extensions: [
            new Table(),
            new TableCell(),
            new TableHeader(),
            new TableRow(),
          ],
          content: ''
        }),
      }
    },
    beforeDestroy() {
      this.editor.destroy()
    }
  }
  </script>
```

## TableHeader
Allows you to use the `<th>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `Table` extension.
:::

## TableCell
Allows you to use the `<td>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `Table` extension.
:::

## TableRow
Allows you to use the `<tr>` HTML tag in the editor.

::: warning Restrictions
This extensions is intended to be used with the `Table` extension.
:::

## TodoItem
It renders a single toggleable item of a list.

::: warning Restrictions
This extensions is intended to be used with the `TodoList` extension. 
:::

## TodoList
Renders a toggleable list of items. It should be used with the `TodoItem` extension.

::: warning Restrictions
This extensions is intended to be used with the `TodoItem` extension. 
:::

## Strike
Allows you to use the `<s>` HTML tag in the editor.

## Underline
Allows you to use the `<u>` HTML tag in the editor.

[@tiptap-contrib]: https://github.com/scrumpy/tiptap/blob/master/CONTRIBUTING.md
[@npmjs-tiptap-commands]: https://npmjs.org/package/tiptap-commands