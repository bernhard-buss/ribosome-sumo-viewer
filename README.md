# Ribosome SUMO Viewer

**Open the viewer:** https://bernhard-buss.github.io/ribosome-sumo-viewer/

A single-page browser viewer for the SUMO2/3 acceptor sites of the cytosolic
ribosomal proteins on structures of the human ribosome. Each modified lysine is
shown on the structure and coloured by its response to proteasome inhibition
(MG132) or heat shock, or by its environment in the particle (exposed, in
contact with rRNA, buried). A table lists every site; selecting a row focuses
the structure on that lysine.

In the structure, hovering identifies a residue, a click or tap marks it and
pins its label, and a double click zooms to it without cutting anything away.
*Focus* and *Overview* at the bottom right switch between a close-up of the
marked residue — in which whatever lies in front of it fades with distance,
a peek hole that follows the camera — and the whole structure.

## Structures

The *Structure* menu offers seven states of the ribosome; the address takes the
PDB code (`?s=8G60`), and without it the page opens on the mature 80S.

| Structure | PDB | What it is |
|---|---|---|
| Mature 80S | [8QOI](https://www.rcsb.org/structure/8QOI) | vacant ribosome at 1.9 Å; the reference for the statistics |
| Decoding 80S | [8G60](https://www.rcsb.org/structure/8G60) | translating: mRNA, A- and P-site tRNA, eEF1A; resolves the L1 stalk |
| Idle 80S | [8XSX](https://www.rcsb.org/structure/8XSX) | with eEF2, SERBP1, EBP1 and E-site tRNA |
| Collided disome | [9RPV](https://www.rcsb.org/structure/9RPV) | a stalled ribosome and the one that ran into it, with ZAK and EDF1 |
| Nucleolar pre-60S | [8FKV](https://www.rcsb.org/structure/8FKV) | early assembly intermediate of the large subunit |
| Nuclear pre-60S | [8FLE](https://www.rcsb.org/structure/8FLE) | late nuclear assembly intermediate of the large subunit |
| Late pre-40S | [6ZXG](https://www.rcsb.org/structure/6ZXG) | late assembly intermediate of the small subunit |

All single particles are superposed on the mature 80S, so the view buttons show
the same face in each. Factors, tRNA and mRNA are drawn in their own colours and
can be hidden. The details of a site give its environment in every other
structure, with a link that opens that structure at the site.

Everything runs in the browser. The structure is fetched from the PDB by the
browser; nothing is uploaded.

## Room for SUMO

An exposed lysine can be reached by water, which does not say whether a SUMO
fits there. For every site in every structure the viewer gives the share of
placements of the SUMO2 core (PDB [1WM3](https://www.rcsb.org/structure/1WM3)),
on its flexible tether, that overlap nothing: *room*, *tight* or *none*. The
same placements are tested without the partners, without the other ribosome
and on the subunit alone, which names what takes the room away. The colouring
*Room for SUMO* paints the classes, and the details of a site can draw a SUMO
at one of the placements that fit. The model is checked on a crystal structure
of a SUMO2 conjugate ([3UIO](https://www.rcsb.org/structure/3UIO)); the help
topic *Room for SUMO* has the method and its limits.

## Sharing a view

The address of the page holds what is shown: structure, colouring, hidden
partners, filters, sorting, the selected site, a SUMO drawn at it, and the
view (a standard view, or the camera as it was turned and zoomed). It is
updated as you go; *Copy link* copies it. For example
`?s=9RPV&colour=room&site=RACK1+K264&ribosome=stalled&sumo=1` opens the
collided disome coloured by room for SUMO, with that site selected and a SUMO
drawn at it. A table of your own is never part of a link.

## The free protein

Every site also has the AlphaFold DB model of its protein alone: how much
room a SUMO has there and how confident the model is at the lysine (pLDDT).
*Show the free protein* in the detail card replaces the ribosome with that
model, with the sites in the current colouring and, if asked for, a SUMO
placed at the selected site; the protein can be coloured by confidence. The
colouring *Room on the free protein* compares with *Room for SUMO* on the
particle.

## Help and versions

The **Help** button (or the `?` key) opens the in-page help: nine topics, a
search box, and the changelog. Every ⓘ on the page opens the help at the entry
for the control next to it, and an open entry has its own address
(`#help/topic/entry`) that can be shared.

The version next to the title is raised with every change of what the viewer
can do; [CHANGELOG.md](CHANGELOG.md) is the one place the history is written,
and the help renders that file.

## Statistics

The **Statistics** button (or the address `#stats`) opens the results of the
analysis behind the data: the modified lysines against the other lysines of the
same proteins, the subunits and four regions of the ribosome, spatial
clustering tested by random draws, the hotspots of MG132-responsive sites, and
other modifications recorded at the same lysines in UniProt. *Show* buttons set
the matching colouring and filter. For the other structures the window shows
what that state adds: the sites near its factors, tRNA and mRNA tested against
the other lysines, and for the assembly intermediates the fate of the lysines
that the mature ribosome encloses. The results are stored in
`data/<PDB code>/stats.json`; the page displays them and does not recompute them.

## Your own data

*Load a table…* reads a CSV or TSV from your disk into the page and colours the
structure with it. The file is processed in the browser: it is not uploaded and
not stored, and it is gone when the page is closed.

- A `gene` (symbol) or `protein` (UniProt accession) column identifies the
  ribosomal protein; every other column is a value column.
- Rows without a `position` colour the whole protein (*Colour the proteins by*).
- Rows with a `position` colour that lysine, if it is one of the listed sites
  (*Colour the sites by*).
- Numeric columns get a colour ramp (diverging when the values span zero),
  text columns one colour per category. The active column is also shown in the
  site table and in the detail card.

## Data

| File | Content |
|---|---|
| `data/structures.json` | the structures of the menu |
| `data/placement.json` | the environment of every site in every structure |
| `data/<PDB code>/sites.json` | one row per site: protein, position, structural annotation (environment, region, hotspot, nearest partner, room for SUMO with a placement), quantification, other modifications |
| `data/<PDB code>/stats.json` | the stored test results shown in the Statistics window |
| `data/<PDB code>/annotations.json` | per-residue colours and tooltips for the structure view |
| `data/<PDB code>/scene_*.mvsj` | one [MolViewSpec](https://molstar.org/mol-view-spec/) scene per colouring |
| `data/<PDB code>/meta.json` | chains, colourings, legends, partners and the standard views |
| `data/free/<accession>.json` | the AlphaFold DB model of one ribosomal protein: confidence per residue, its lysines with room for SUMO and a placement |

Sources:

- **Sites and quantification** — Hendriks IA et al., *Site-specific
  characterization of endogenous SUMOylation across species and organs*,
  Nat Commun 9:2456 (2018), Supplementary Data 1 (CC BY 4.0). HEK293 cells;
  control, MG132 and heat shock; Z-scores, log2 fold changes and q-values as
  published.
- **Structures** — the PDB entries of the table above; the reference is
  [8QOI](https://www.rcsb.org/structure/8QOI), human 80S ribosome at 1.9 Å
  (Holvec S et al., Nat Struct Mol Biol 31:1251, 2024). The publication of each
  entry is linked from its PDB page.
- **Free proteins** — [AlphaFold DB](https://alphafold.ebi.ac.uk) models
  (AlphaFold 2 monomer predictions, model version 6; CC-BY 4.0), fetched by
  the browser from the AlphaFold DB when a free protein is shown.
- **Other modifications** — the cross-link and modified-residue records of
  UniProt (CC BY 4.0) for the proteins of the structure.
- **Structural annotation** — computed from each structure: a lysine is *rRNA
  contact* when its side-chain nitrogen (NZ) is within 4 Å of an rRNA atom,
  *exposed* when it is not and its NZ has ≥ 10 Å² of solvent-accessible surface
  in the particle, *buried* otherwise, and *not modelled* when the residue has
  no coordinates. A site is *near a partner* when its NZ is within 10 Å of a
  factor, a tRNA, the mRNA or the other ribosome of the disome. A structure
  lists the sites of the ribosomal proteins it contains.

## Development

The viewer is `index.html` (HTML + CSS + JS, no build step) plus `CHANGELOG.md`
and the files in `data/`; [Mol*](https://molstar.org) is loaded from a CDN at a pinned version.
Serve the folder with any static server and open `index.html`.

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 ETH Zurich.
