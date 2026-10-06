# Changelog

The version next to the title is raised with every change of what the viewer can do: the
minor number for new features, the patch number for smaller changes and fixes. The entries
say what changed for the person using the viewer. This file is the only place the history is
written; the Changelog page of the in-page help renders it.

## 0.7.1 — 2026-10-06
Clicking in the structure. A click (or tap) marks the residue and pins its label at the top
left of the structure, where it stays until the next click; a SUMO site is also selected in the
table, with its details below it. A double click (or double tap) zooms to the residue. Hovering
keeps showing the label at the bottom right as before.

- Before, a single click moved the camera onto the residue and cut away everything in front
  of and behind it. This no longer happens, also not when a site is chosen in the table: the
  camera moves closer and nothing is cut away.
- A click on empty space removes the mark.
- Choosing a site no longer scrolls the page on a narrow screen; only the table scrolls.

## 0.7 — 2026-10-05
Shareable links. The address of the page now holds everything that is chosen, and a
*Copy link* button at the top copies it: a link opens the viewer in the same state.

- In the link: the structure, the colouring of the sites, hidden partners, the search text
  and the three filter menus with the MG132 checkbox, the sorting of the table, the selected
  site and a SUMO drawn at it, and the view — a standard view by name, or the camera exactly
  as it was turned and zoomed. An open Help entry or the Statistics window stays in the link
  as before. Defaults are left out, so the opening view has the bare address.
- Not in the link: a table of your own and the protein colouring by it; the file never
  leaves your computer.
- Fix: since 0.5 the opening view of a structure was drawn about a third farther away than
  the same view chosen with its button; both now match.
- Help: *Sharing a view*; the topic *Room for SUMO* explains the measure with a picture and a
  sense of scale.

## 0.6 — 2026-10-05
Room for SUMO. For every site in every structure the viewer now says whether a SUMO fits at
the lysine: the core of SUMO2 is placed on its tether in many ways, and the share of
placements that overlap nothing is the measure (classes room, tight, none).

- New site colouring *Room for SUMO* and matching filters, including *room taken by* the
  partners, the other ribosome or the other subunit.
- The detail card gives the share of placements that fit, also without the partners, on the
  ribosome alone and on the subunit alone, and can draw a SUMO at the site: at a placement
  that fits, or, where the room is taken, where it would sit without what is in its way.
- The Statistics window has a section *Room for SUMO* for every structure: the classes among
  sites and other lysines, the sites by environment, the tests on the mature 80S, and the
  sites whose room something takes.
- New help topic *Room for SUMO* (measure, method with its test on a crystal structure of a
  SUMO2 conjugate, what takes the room, showing a SUMO, limits).

## 0.5 — 2026-10-05
Seven structures. A *Structure* menu offers, beside the mature 80S, a decoding and an idle
80S, a pair of collided ribosomes, two pre-60S particles and a pre-40S particle. Each has its
own picture, site table and Statistics window; the colouring, the selected site and a loaded
table carry over, and the address (`?s=` and the PDB code) can be shared. All single
particles are superposed on the mature 80S, so a view button shows the same face in each.

- The decoding 80S shows the sites of the L1 stalk (RPL10A), RPL10 and RPL12, the pre-60S
  particles those of RPL7L1; these proteins are not part of the mature structure.
- Factors, tRNA and mRNA are drawn in their own colours and can be hidden. In the disome the
  collided ribosome is paler than the stalled one, and every site is listed once per ribosome.
- New site colourings: *Near a partner* (the nearest factor, tRNA, mRNA or other ribosome
  within 10 Å) and *Environment in the mature 80S*. New filters: near a partner, on one
  ribosome of the disome, exposed here and enclosed in the mature 80S, resolved here and not
  in the mature 80S.
- The detail card names the nearest partner and, under *Elsewhere*, gives the environment of
  the same lysine in every other structure; a name there opens that structure at the site.
- The Statistics window of the other structures: what the structure holds and adds, the test
  of SUMO sites against other lysines near each kind of partner with the list of sites, and
  for the assembly intermediates the fate of the lysines that the mature ribosome encloses.
- If the data of a chosen structure cannot be fetched, the structure on screen stays, the
  menu returns to it, and the message names what failed; a click dismisses the message.
- New help topic *Structures*; new entries for the two colourings and the statistics of the
  other structures; the entries on environment, table, details and methods now cover all
  structures.

## 0.4.1 — 2026-10-05
Fixes.

- *Show* on a hotspot in the Statistics window now turns the structure to that hotspot; in
  0.4 it set the colouring and the filter but left the view unchanged.
- Choosing a colouring, a *Show* button or a table while the structure is still loading no
  longer starts a second load on top of the first, which could leave the view empty.

## 0.4 — 2026-10-05
Statistics. A Statistics window (button in the header, or the address `#stats`) shows the
results of the analysis behind the data: the modified lysines against the other lysines of
the same proteins, the two subunits and four regions of the ribosome, spatial clustering
tested by random draws, the hotspots of MG132-responsive sites, and other modifications
recorded at the same lysines. Each table has an ⓘ to its method, and *Show* buttons set
the matching colouring and filter (for a hotspot also the view).

- Three new site colourings: region (40S head, 40S body, 60S central protuberance, 60S
  body), hotspots, and other modifications recorded in UniProt. The colourings are now
  grouped into *Response to stress* and *Position and context*.
- The site table shows the region instead of the subunit and can be filtered by region,
  hotspot, subunit interface and other modification; the detail card adds the region, the
  distance to the other subunit, the hotspot and the other modifications.
- New help topic *Statistics*; new entries for the three colourings.
- Data: `data/stats.json` (the stored results) and new fields in `data/sites.json`
  (`region`, `interface`, `dist_other_subunit`, `hotspot`, `other_mods`).
- Fix: a protein encoded by several genes (RPL9) is listed under its first gene symbol, so
  that a loaded table matches it by gene name.

## 0.3 — 2026-10-04
Help. A Help window (button in the header, or the `?` key) with seven topics and this
changelog; a search box finds entries across all topics. Every ⓘ on the page opens the
help at the entry for the control next to it — the ⓘ beside *Colour the sites by* follows
the active colouring. An open entry has its own address (`#help/topic/entry`) that can be
copied and shared. The version next to the title opens the changelog and shows *new*
after an update until it has been opened.

## 0.2 — 2026-10-04
Your data. *Load a table…* reads a CSV or TSV from the visitor's computer inside the
browser — nothing is uploaded or stored.

- Rows without a position colour whole proteins (*Colour the proteins by*); rows with a
  position colour that lysine if it is a listed site.
- Numeric columns get a colour ramp (two-sided when the values span zero), text columns
  one colour per category. Protein values use green scales to keep them apart from the
  site colours.
- The active column is added to the site table (sortable) and all columns to the detail
  card. The protein list of the structure is part of `data/meta.json` for the matching.
- Selecting a site also outlines it in the structure.

## 0.1 — 2026-10-04
First version. The human 80S ribosome (PDB 8QOI) with the SUMO2/3 sites of its proteins
from Hendriks et al. 2018: 234 sites on 54 proteins, 214 of them modelled.

- Five site colourings: MG132 fold change, Z-score in control, MG132 and heat shock,
  lysine environment (exposed, rRNA contact, buried).
- Six standard views derived from the structure's geometry.
- Site table with search, filters and sorting; selecting a site centres the structure
  on it and shows its details.
