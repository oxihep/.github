# oxihep

**Pure-Rust tools for high-energy physics** — read and write ROOT files,
fill histograms, fit, compute statistics and make publication plots, with no
C++ ROOT, no Python and no system libraries. The crates are split the way
Python's [Scikit-HEP](https://scikit-hep.org) is: each works on its own, and
together they cover an analysis from the file to the figure.

oxihep is a personal project, developed by one person for now. Issues and
pull requests are welcome on any of the repositories.

<p align="center">
  <img src="https://raw.githubusercontent.com/oxihep/oxiroot/main/docs/images/plot-mplhep.png" alt="A Z → μμ mass peak in the mplhep style, with a Gaussian fit and its statistics box" width="48%">
  <img src="https://raw.githubusercontent.com/oxihep/oxiroot/main/docs/images/plot-ratio.png" alt="A filled MC histogram with data points over a data/MC ratio panel" width="48%">
</p>

## The crates

| Crate | What it does | Python counterpart | Latest | Docs |
| --- | --- | --- | --- | --- |
| [**oxiroot**](https://github.com/oxihep/oxiroot) | Read and write ROOT files: `TTree`, RNTuple, histograms, graphs; local, HTTP and `root://` (XRootD). Verified against ROOT C++ and uproot. Re-exports the crates below. | uproot | ![tag](https://img.shields.io/github/v/tag/oxihep/oxiroot?label=) | [guide](https://oxihep.github.io/oxiroot/) |
| [**oxihist**](https://github.com/oxihep/oxihist) | Histograms: typed axes (regular, variable, integer, category, boolean), weighted, mean and profile storages, threaded filling | boost-histogram, hist | ![tag](https://img.shields.io/github/v/tag/oxihep/oxihist?label=) | [API](https://oxihep.github.io/oxihist/) |
| [**oxiplot**](https://github.com/oxihep/oxiplot) | Plots to SVG, PNG and PDF with a matplotlib-like API and the mplhep look; TeX math labels, log axes, stacks, ratio plots, limit bands, pulls and impacts | matplotlib, mplhep | ![tag](https://img.shields.io/github/v/tag/oxihep/oxiplot?label=) | [API](https://oxihep.github.io/oxiplot/) |
| [**oxifit**](https://github.com/oxihep/oxifit) | Fitting with a pure-Rust Minuit2 (MIGRAD, MINOS): binned and unbinned fits, CLs limits, HistFactory-style template fits, sWeights, MCMC sampling; fits to any ROOT formula | iminuit, pyhf, emcee | ![tag](https://img.shields.io/github/v/tag/oxihep/oxifit?label=) | [API](https://oxihep.github.io/oxifit/) |
| [**oxiformula**](https://github.com/oxihep/oxiformula) | ROOT's `TFormula`: parse, evaluate, compile and differentiate formulas, with ROOT's parameters, shortcuts and functions; checked against ROOT | ROOT's `TFormula` | ![tag](https://img.shields.io/github/v/tag/oxihep/oxiformula?label=) | [API](https://oxihep.github.io/oxiformula/) |
| [**oxistats**](https://github.com/oxihep/oxistats) | Statistics verified against scipy: distributions, hypothesis tests, special functions, HEP lineshapes, confidence intervals | scipy.stats, hepstats | ![tag](https://img.shields.io/github/v/tag/oxihep/oxistats?label=) | [API](https://oxihep.github.io/oxistats/) |
| [**oxiparticle**](https://github.com/oxihep/oxiparticle) | PDG particle data and Monte Carlo particle-ID decoding | particle | ![tag](https://img.shields.io/github/v/tag/oxihep/oxiparticle?label=) | [API](https://oxihep.github.io/oxiparticle/) |

## Start here

Most analyses need only **oxiroot**, which brings the others in as
`oxiroot::hist`, `oxiroot::plot`, `oxiroot::fit`, `oxiroot::stat` and
`oxiroot::particle`. The crates are not on crates.io yet: depend on them from
GitHub, pinned to a release tag (shown in the table above):

```toml
[dependencies]
oxiroot = { git = "https://github.com/oxihep/oxiroot", tag = "v0.11.0" }
```

```rust
use oxiroot::prelude::*;

let file = FileReader::open("events.root")?;
let tree = TreeReader::open(&file, "Events")?;
let pt = tree.read_branch(&file, "Muon_pt")?;
```

The [oxiroot guide](https://oxihep.github.io/oxiroot/) walks through reading
and writing files, histograms, fitting, statistics and plotting.

## How they fit together

Each crate depends only on what it needs, so a histogram-only or
statistics-only project pulls in nothing else:

- **oxiroot** uses all of the others.
- **oxihist** can draw with oxiplot (`plot` feature) and fit with oxifit
  (`fit` feature).
- **oxiplot** can overlay oxifit models (`fit` feature).
- **oxifit** uses oxiformula and oxistats.
- **oxiformula** uses oxistats.
- **oxistats** and **oxiparticle** depend on no other oxihep crate.

All of them are safe Rust (`unsafe_code = "deny"`), tested on Linux and macOS,
and need Rust 1.100 or newer.

## AI assistance

These crates are developed with the help of AI coding assistants. Under the
author's direction they wrote and reviewed much of the code, the tests and
the documentation. Every change goes through the same checks either way —
each repository's test suite and CI, cross-checks against ROOT C++, uproot
and scipy where they apply, and review before merging. If something looks
wrong, please open an issue on the repository concerned.

## Status

Pre-1.0 and actively developed: APIs may still change between minor
versions, and each release says what changed in its changelog. What comes next is in the
[roadmap](https://github.com/oxihep/oxiroot/blob/main/ROADMAP.md).
Licensed under MIT; see each repository for third-party notices.
