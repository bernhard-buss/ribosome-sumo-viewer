# Changelog

The version next to the title is raised with every change of what the viewer can do.
Changes of the data files are listed with the version that shipped them. This file is
the only place the history is written; the Changelog page of the in-page help renders it.

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
