# Changelog

The version next to the title is raised with every change of what the viewer can do.
Changes of the data files are listed with the version that shipped them. This file is
the only place the history is written; the Changelog page of the in-page help renders it.

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
- Data: one folder per structure (`data/<PDB code>/`), `data/structures.json` (the menu) and
  `data/placement.json` (each site's environment in each structure). The files of the mature
  80S moved from `data/` to `data/8QOI/`.

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
