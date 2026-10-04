# Ribosome SUMO Viewer

**Open the viewer:** https://bernhard-buss.github.io/ribosome-sumo-viewer/

A single-page browser viewer for the SUMO2/3 acceptor sites of the cytosolic
ribosomal proteins on the human 80S ribosome. Each modified lysine is shown on
the structure and coloured by its response to proteasome inhibition (MG132) or
heat shock, or by its environment in the assembled ribosome (exposed, in
contact with rRNA, buried). A table lists every site; selecting a row centres
the structure on that lysine.

Everything runs in the browser. The structure is fetched from the PDB by the
browser; nothing is uploaded.

## Help and versions

The **Help** button (or the `?` key) opens the in-page help: seven topics, a
search box, and the changelog. Every ⓘ on the page opens the help at the entry
for the control next to it, and an open entry has its own address
(`#help/topic/entry`) that can be shared.

The version next to the title is raised with every change of what the viewer
can do; [CHANGELOG.md](CHANGELOG.md) is the one place the history is written,
and the help renders that file.

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
| `data/sites.json` | one row per site: protein, position, structural annotation, quantification |
| `data/annotations.json` | per-residue colours and tooltips for the structure view |
| `data/scene_*.mvsj` | one [MolViewSpec](https://molstar.org/mol-view-spec/) scene per colouring |
| `data/meta.json` | colourings, legends and the six standard views |

Sources:

- **Sites and quantification** — Hendriks IA et al., *Site-specific
  characterization of endogenous SUMOylation across species and organs*,
  Nat Commun 9:2456 (2018), Supplementary Data 1 (CC BY 4.0). HEK293 cells;
  control, MG132 and heat shock; Z-scores, log2 fold changes and q-values as
  published.
- **Structure** — PDB [8QOI](https://www.rcsb.org/structure/8QOI), human 80S
  ribosome at 1.9 Å (Holvec S et al., Nat Struct Mol Biol 31:1251, 2024).
- **Structural annotation** — computed from 8QOI: a lysine is *rRNA contact*
  when its side-chain nitrogen (NZ) is within 4 Å of an rRNA atom, *exposed*
  when it is not and its NZ has ≥ 10 Å² of solvent-accessible surface in the
  assembled particle, *buried* otherwise, and *not modelled* when the residue
  has no coordinates. Sites on proteins absent from 8QOI (the mobile stalks)
  are not listed.

## Development

The viewer is `index.html` (HTML + CSS + JS, no build step) plus `CHANGELOG.md`
and the files in `data/`; [Mol*](https://molstar.org) is loaded from a CDN at a pinned version.
Serve the folder with any static server and open `index.html`.

## License

MIT — see [LICENSE](LICENSE). Copyright (c) 2026 ETH Zurich.
