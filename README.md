# Grid System

**Grid System** is a lightweight, breakpoint free, completely responsive, element query driven\*, progressive enhancement based CSS grid framework. It exists in this `README.md` file, in the section titled **The CSS** (below).

Just edit the lines marked 'edit me!' to your requirements and write an HTML structure like the one illustrated in the section titled **The HTML** (also below).

(\* Not really, but kind of. See **3** under **Notes**, below.)

## The CSS

```css
.grid-container {
  display: flex; /* 1 */
  flex-wrap: wrap; /* 2 */
  margin: -0.5em; /* 5 (edit me!) */
}

.grid > * {
  flex: 1 0 5em; /* 3 (edit me!) */
  margin: 0.5em; /* 4 (edit me!) */
}
```

## The HTML

```html
<div class="grid-container"> <!-- 6 -->
  <ul class="grid">
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
    <li><!-- grid cell/item/child/whatever --></li>
  </ul>
</div>
```

## Notes

1. **Grid System** is a Flexbox based grid system. Even Opera Mini supports Flexbox. Older user agents that don't support Flexbox ignore the `display: flex` declaration, degrading to a single column layout. No harm done.
2. This line determines how items are handled. The `wrap` value means items will start a new row if there's not enough room on the current one.
3. This is the 'element query' part. Instead of setting an arbitrary number of columns and using breakpoints, we decide roughly how wide we want the item to be (`5em` in the example — the flex basis) and make sure items can grow to use the available space (`1`) but not shrink (`0`). So only change the `5em` value and leave `1 0` as it is.
4. This is for gutters. A `0.5em` margin here means gutters of `1em` (the margins double up).
5. This should always be a negative version of **4**. It compensates for the margins created by the items. It makes sure the outside of the `.grid` container remains flush horizontally and no additional margin is added to the vertical flow.
6. The `class="grid-container"` container in the HTML snippet enables you to add positive margins around the grid — not possible with just `.grid` because this uses negative margins (see **5**). It also suppresses horizontal scrolling issues which occur under certain circumstances.

## Items with different widths

Sometimes you want certain items to be narrower or wider. Maybe you want the fifth item to always be approximately twice the size of a regular item (where space permits). If the regular `flex-basis` is `5em`, then&hellip;

```css
.grid > *:nth-child(5) {
  flex-basis: 10em;
}
```

Don't worry, flexbox will make sure there aren't any gaps.

### Percentage widths

You can choose a percentage based width for individual items, but remember to adjust for the gutter margin with by subtracting it using `calc`. For example, to make the first item 100% in width when the gutter width is `1em`, use:

```css
.grid > *:first-child {
  flex-basis: calc(100% - 1em);
}
```

**Warning:** Internet Explorer [does not respect `box-sizing`](https://github.com/philipwalton/flexbugs/issues/3#issuecomment-69036362) on `flex-basis` items. In which case, if you use percentage widths, you cannot pad the flex item directly. You will need to insert child nodes inside flex items and pad them instead.

```html
<div class="grid-container"> <!-- 6 -->
  <ul class="grid">
    <li>
      <div><!-- pad this --></div>
    </li>
  </ul>
</div>
```

## RTL Grids

Flexbox supports `rtl` already. Just add `dir="rtl"` to the `.fukol-grid` element and the flex direction will automatically be reversed.
