# floorplan# Floor plan

A floor plan editor that runs entirely in the browser. Draw rooms, drop in furniture,
drag everything around, and save the result as a file or a picture.

One file, no build step, no dependencies, no server.

## Put it online with GitHub Pages

1. Create a new repository on GitHub (public, and tick nothing else).
2. Upload `index.html` to the root of the repository.
3. Go to **Settings → Pages**.
4. Under **Source** choose **Deploy from a branch**, pick the `main` branch and the `/ (root)` folder, then save.
5. Wait a minute or two. Your plan lives at `https://YOUR-USERNAME.github.io/YOUR-REPO/`.

Any change you push to `index.html` goes live automatically a minute later.

To work on it without GitHub, just open `index.html` from your own computer — everything works offline.

## Using it

**Adding things.** Click anything in the left column and it appears in the middle of your view.
Rooms, walls, doors and windows are under Structure; the rest is furniture, grouped by
which room it usually lives in.

**Moving things.** Drag them. Drag on empty space to select several at once, or hold shift
and click to add to a selection.

**Resizing.** Select one item and drag a corner or edge handle. The knob above it turns the item.
Or type exact sizes into the panel on the right — it understands `12`, `12.5`, `12' 6"` and `12-6`.

**Getting around.** Scroll to zoom, hold space and drag to pan, or drag with the right mouse
button. On a phone or tablet, pinch to zoom and drag with two fingers. The percentage in the
top bar fits the whole plan back on screen.

### Keyboard

| | |
|---|---|
| `Ctrl`/`Cmd` + `Z` | Undo |
| `Ctrl`/`Cmd` + `Shift` + `Z` | Redo |
| `Ctrl`/`Cmd` + `D` | Duplicate |
| `Ctrl`/`Cmd` + `A` | Select everything |
| `Ctrl`/`Cmd` + `S` | Save the plan file |
| `Delete` | Remove |
| `R` | Turn 90° |
| `G` | Grid snapping on or off |
| `[` and `]` | Send back, bring forward |
| Arrow keys | Nudge (hold shift for a bigger step) |

## Saving your work

Your plan is **not** kept automatically — closing the tab loses it. Press **Save** (or `Ctrl`+`S`)
to download a `.json` file, and **Open** to load it back later. Keep that file in the repository
if you want the plan to travel with the site.

**Picture** exports a high-resolution PNG of just the drawing, with no grid or handles —
good for sending to a builder or dropping into a document. **Print** lays the plan out on paper.

## Changing it

Everything lives in `index.html`.

**Add your own furniture.** Find the `SYMBOLS` object and add an entry. Shapes are drawn in
their own box, from `(0,0)` to `(w,h)`, in feet:

```js
deskLamp: {
  name: 'Desk lamp', cat: 'Bedroom', w: 1, h: 1,
  draw: (w, h) => ci(w/2, h/2, w/2, '#ffffff') + ci(w/2, h/2, w/6, null, 1)
},
```

Then add a matching 22×22 line drawing to `ICONS` under the same key so it appears in the
left column. The helpers `r`, `rr`, `ln`, `ci`, `el` and `pa` cover rectangles, rounded
rectangles, lines, circles, ellipses and paths.

**Colours** are the CSS variables at the top of the file. `--paper` is the canvas,
`--ink` the panels, `--brass` the selection colour. The fills offered in the properties
panel are the `PALETTE` array.

**Line weights** are real thicknesses in feet, so the drawing behaves like paper when you
zoom. `WALL` is `0.5` — a six-inch wall. `LW` is the weight of one thin line.

**Grid spacing** is `state.grid`, in feet. `0.5` means everything snaps to six inches.

## Notes

Distances are held internally in feet; the Feet/Metres button only changes how they are
shown and typed, so switching units never moves anything.
