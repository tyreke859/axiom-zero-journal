# SOURCES — curated, freely accessible primary/research sources

Checked from the box with curl on **2026-10-31 at 7:18 PM PDT** (`tools/fetch_check.sh` re-runs the check; the raw results are in `notes/url_results.txt`).
Legend: ✅ 200 OK · ⚠️ reachable but blocks curl (403/412/202) — **use a browser or the API listed** · ⏳ timed out from the box (not a 404; may be network/geo) · 🔑 key optional/recommended.
No URL returned 404, so none were dropped.

**Rule:** for a claim, prefer the paper, dataset, or official table over a press release or a summary. Cite the exact URL plus the version or date you accessed.

## Literature search and metadata
| Source | Status | Programmatic use (shell) |
|---|---|---|
| arXiv: https://arxiv.org | ✅ | `tools/arxiv_search.py "query"`. Raw: `curl "https://export.arxiv.org/api/query?search_query=all:entropy&max_results=5"`. **Use https**, because plain http returned 500. Be polite: ≤1 req/3 s. |
| OpenAlex: https://api.openalex.org | ✅ | `tools/paper_lookup.py search|doi|cites`. Raw: `curl "https://api.openalex.org/works?search=dark%20matter&per-page=5"`. Filters: `filter=cites:W…`, `from_publication_date:`. No key. |
| Semantic Scholar: https://api.semanticscholar.org/graph/v1 | ✅/429 🔑 | `tools/paper_lookup.py search "q" --src s2`. The shared IP gets rate-limited often (we got 429 several times), so fall back to OpenAlex. |
| Crossref: https://api.crossref.org | ✅ | `curl "https://api.crossref.org/works?query=quantum+decoherence&rows=5"`. Use it for DOI metadata and to check whether a reference exists. |
| Unpaywall: https://api.unpaywall.org/v2/DOI?email=… | ✅ | Legal OA copy of a DOI. Needs a real-looking email (example.com → 422). |
| Europe PMC: https://www.ebi.ac.uk/europepmc/webservices/rest | ✅ | `curl "https://www.ebi.ac.uk/europepmc/webservices/rest/search?query=crispr&format=json&pageSize=5"`. Also returns full text for OA papers. |
| PubMed / NCBI E-utilities: https://eutils.ncbi.nlm.nih.gov/entrez/eutils/ | ✅ | `esearch.fcgi?db=pubmed&term=…&retmode=json`, then `efetch.fcgi?db=pubmed&id=…&rettype=abstract`. ≤3 req/s. |
| bioRxiv / medRxiv: https://api.biorxiv.org | ✅ | `curl https://api.biorxiv.org/details/biorxiv/2026-10-01/2026-10-31/0` (date-range feed). Use OpenAlex for keyword search. |
| NASA ADS: https://ui.adsabs.harvard.edu | ⚠️ 202 (JS app) 🔑 | The API needs a free token (`api.adsabs.harvard.edu/v1/search/query`). Otherwise use arXiv or OpenAlex for astro. |
| INSPIRE-HEP: https://inspirehep.net/api | ✅ | `curl "https://inspirehep.net/api/literature?q=title%20inflation&size=5"` (HEP plus citations). |
| zbMATH Open: https://api.zbmath.org | ✅ | `curl "https://api.zbmath.org/v1/document/_search?search_string=collatz&results_per_page=5"`. |
| DOAJ: https://doaj.org | ⚠️ homepage 403; ✅ API | `curl https://doaj.org/api/search/articles/entropy`. |
| CORE: https://core.ac.uk · Internet Archive Scholar: https://scholar.archive.org | ✅ | Find OA full texts. |
| OSTI (US DOE): https://www.osti.gov · NASA NTRS: https://ntrs.nasa.gov | ✅ | Technical reports. |
| ClinicalTrials.gov: https://clinicaltrials.gov/api/v2 | ✅ | `curl "https://clinicaltrials.gov/api/v2/studies?query.term=psilocybin&pageSize=5"`. Use it to check for pre-registration and outcome switching. |
| Cochrane: https://www.cochranelibrary.com | ⚠️ 412 to curl | Browser only. Systematic reviews. |

## Mathematics
| Source | Status | Use |
|---|---|---|
| OEIS: https://oeis.org | ✅ | `curl "https://oeis.org/search?q=1,1,2,5,14,42&fmt=json"`. Identify a sequence produced by computation. |
| LMFDB: https://www.lmfdb.org | ✅ | L-functions, modular forms, elliptic curves, number fields (also has an API at `/api/`). |
| DLMF (NIST): https://dlmf.nist.gov | ✅ | Authoritative special-function identities. |
| MathWorld: https://mathworld.wolfram.com · nLab: https://ncatlab.org | ✅ | Secondary references. Verify against primary papers. |
| MathOverflow via StackExchange API: https://api.stackexchange.com/2.3 | ✅ | `…/search?intitle=riemann&site=mathoverflow`. Expert discussion counts as evidence, not proof. |
| Prime Pages: https://t5k.org | ✅ | Prime records. |
| Erdős problems: https://www.erdosproblems.com | ✅ (curl 200, `/N` problem pages, 2026-10-31) | Status of the Erdős problems, including AI-assisted solutions. |
| Erdős problems database (Tao): https://github.com/teorth/erdosproblems | ✅ | `data/problems.yaml` gives status, tags and Lean links for all 1221 problems. `data/statistics_history.csv` is the solved-count time series. Since 2026-10-06 the site hides solved counts. |
| AI contributions wiki: https://github.com/teorth/erdosproblems/wiki/AI-contributions-to-Erd%C5%91s-problems | ✅ (frozen at 2026-06-30) | It sorts AI results by section: standalone, with literature, building on literature, collaborative, literature search, formalization. The raw markdown is at `raw.githubusercontent.com/wiki/teorth/erdosproblems/<page>.md`. It is the best low-bias sample for T01. |
| Formal Conjectures (DeepMind): https://github.com/google-deepmind/formal-conjectures | ✅ | Lean statements of open problems and disproofs (e.g. Jacobian PR #4474). Check PR merge status via the GitHub API. |
| Primary AI transcripts (ChatGPT share links cited in papers) | ✅ (curl 200 with browser UA; the JSON is embedded in the HTML) | e.g. #1196 transcript (arXiv 2605.00301 fn 12), saved at `data/gpt54pro_1196_transcript.html`. Extract user turns and thought summaries with regex over the serialized strings. This is the best evidence for who-contributed-what. |
| Erdős forum threads: https://www.erdosproblems.com/forum/thread/N | ✅ (curl 200) | Expert comments (Tao and others), links to AI write-ups (e.g. cdn.openai.com PDFs) and Lean proofs. Bibliography keys like [APSSV26b] load via JS and are not in static HTML. |
| Secret Blogging Seminar (sbseminar.wordpress.com) | ✅ (curl 200) | Expert math blog. The comment threads hold primary-source discussion, e.g. the Jacobian explanation (E014). |
| AlphaEvolve problem repository: https://google-deepmind.github.io/alphaevolve_repository_of_problems/ | ✅ (via search) | Prompts, verifiers, and evolved programs for 67 problems. |

## Philosophy and conceptual
| Stanford Encyclopedia of Philosophy https://plato.stanford.edu ✅ · Internet Encyclopedia of Philosophy https://iep.utm.edu ✅ · PhilPapers https://philpapers.org ⚠️ 403 to curl (use a browser) |
|---|

## Physics, chemistry, and constants
| Source | Status | Use |
|---|---|---|
| CODATA constants (NIST): https://physics.nist.gov/cuu/Constants/ | ✅ | Machine-readable: `curl https://physics.nist.gov/cuu/Constants/Table/allascii.txt` |
| NIST Atomic Spectra DB: https://physics.nist.gov/PhysRefData/ASD/lines_form.html | ✅ | Line lists (form-based; supports CSV output). |
| NIST Chemistry WebBook: https://webbook.nist.gov/chemistry/ | ✅ | Thermochemistry and spectra. |
| Particle Data Group: https://pdg.lbl.gov | ✅ | Particle properties and reviews. |
| CERN Open Data: https://opendata.cern.ch | ✅ | LHC datasets. |
| NNDC (BNL): https://www.nndc.bnl.gov | ✅ | Nuclear data (ENSDF, decay). |
| HITRAN: https://hitran.org | ✅ | Molecular spectroscopic lines (free login for bulk data). |
| PubChem PUG-REST: https://pubchem.ncbi.nlm.nih.gov/rest/pug | ✅ | `curl .../compound/name/caffeine/property/MolecularFormula,MolecularWeight/JSON` |
| Materials Project: https://materialsproject.org | ⚠️ 403 to curl 🔑 | Use the API with a free key. |

## Astronomy and cosmology
| Source | Status | Use |
|---|---|---|
| NASA Exoplanet Archive TAP: https://exoplanetarchive.ipac.caltech.edu/TAP/sync | ✅ | `curl "https://exoplanetarchive.ipac.caltech.edu/TAP/sync?query=select+pl_name,pl_rade+from+ps+where+default_flag=1&format=csv"` |
| JPL Horizons: https://ssd.jpl.nasa.gov/api/horizons.api · SBDB: https://ssd-api.jpl.nasa.gov/sbdb.api | ✅ | Ephemerides and small-body data (`?sstr=Ceres`). |
| NASA planetary fact sheets: https://nssdc.gsfc.nasa.gov/planetary/factsheet/ | ✅ | |
| Gaia archive: https://gea.esac.esa.int/archive/ | ✅ | ADQL/TAP queries. `astropy` is in the venv. |
| MAST (Hubble/JWST/TESS): https://mast.stsci.edu · IRSA: https://irsa.ipac.caltech.edu · NED: https://ned.ipac.caltech.edu · HEASARC: https://heasarc.gsfc.nasa.gov | ✅ | |
| SDSS SkyServer DR18: https://skyserver.sdss.org/dr18 | ✅ | SQL search. |
| LAMBDA (CMB data): https://lambda.gsfc.nasa.gov | ✅ | Planck/WMAP products. |
| GWOSC: https://gwosc.org | ✅ | Gravitational-wave strain and event catalogs: `curl https://gwosc.org/eventapi/json/GWTC/` |
| SIMBAD / VizieR (CDS): https://simbad.cds.unistra.fr , https://vizier.cds.unistra.fr | ⏳ timed out twice | Retry later. Mirror: `vizier.cfa.harvard.edu` (untested). |
| Minor Planet Center: https://www.minorplanetcenter.net | ⏳ timed out | Use JPL SBDB instead. |

## Biology, medicine, and neuroscience
| Source | Status | Use |
|---|---|---|
| UniProt REST: https://rest.uniprot.org | ✅ | `curl "https://rest.uniprot.org/uniprotkb/search?query=insulin&size=5&format=json"` |
| RCSB PDB data API: https://data.rcsb.org/rest/v1/core/entry/4HHB | ✅ | Structures. |
| AlphaFold DB: https://alphafold.ebi.ac.uk | ✅ | `/api/prediction/{UniProtID}` |
| Ensembl REST: https://rest.ensembl.org | ✅ | Genes, sequences, variants (`content-type=application/json`). |
| GBIF: https://api.gbif.org/v1 | ✅ | Species and occurrence data. |
| ChEMBL https://www.ebi.ac.uk/chembl/ · InterPro https://www.ebi.ac.uk/interpro/ · Reactome https://reactome.org · STRING https://string-db.org · KEGG https://www.kegg.jp · ENCODE https://www.encodeproject.org · gnomAD https://gnomad.broadinstitute.org | ✅ | |
| OpenNeuro https://openneuro.org · NeuroVault https://neurovault.org · Allen Brain Map https://portal.brain-map.org | ✅ | Neuroimaging and cell-type data. |

### T08 genetic-code error minimisation (added 2026-11-01, free hour 2; E020 sources listed here too for completeness)
| Source | Status | Use |
|---|---|---|
| Massey 2015, Life 5:1301 (OA): https://pmc.ncbi.nlm.nih.gov/articles/PMC4500140/ | ✅ (Europe PMC XML: `https://www.ebi.ac.uk/europepmc/webservices/rest/PMC4500140/fullTextXML`) | Methods of the '213' grow-by-similarity simulation; founders V,A,D,G; "over 25%" / "over 18%" better than SGC. Copy: `notes/free_hour_2/massey2015.txt`. |
| Massey 2008, J Mol Evol 67:510 — https://doi.org/10.1007/s00239-008-9167-4 | 🔒 paywalled (abstract only; Unpaywall: no OA copy) | Original simulation ("22% ... equivalent or superior"). |
| Massey 2016, J Theor Biol 408:237 — https://doi.org/10.1016/j.jtbi.2016.08.022 | 🔒 ScienceDirect blocks curl (Cloudflare); WebFetch timed out | Abstract only via search. |
| Koonin 2017, "Frozen accident pushing 50", RNA Biol (OA): https://pmc.ncbi.nlm.nih.gov/articles/PMC5492144/ | ✅ | Review; summarises 2-1-3 / ambiguity-reduction / coevolution simulations. Copy: `notes/free_hour_2/koonin2017.txt`. |
| Di Giulio 2023, Biosystems 104838 — https://doi.org/10.1016/j.biosystems.2023.104838 | abstract ✅ via Europe PMC (PMID 36657560); full text 🔒 | Critique of Massey 2008 as "partly tautological". |
| Haig & Hurst 1991 + erratum, J Mol Evol — https://pubmed.ncbi.nlm.nih.gov/1960738/ ; doi 10.1007/pl00006591 | snippet only | Table 3 MS values (reproduced exactly in E020). |
| Freeland & Hurst 1998, J Mol Evol 47:238 — https://doi.org/10.1007/pl00006381 ; partial: https://docslib.org/doc/4269450/the-genetic-code-is-one-in-a-million | 🔒 / first pages only | Weights derivation section NOT accessible. |
| Geyer & Madany Mamlouk 2018, PeerJ 6:e4825 (OA) — https://doi.org/10.7717/peerj.4825 | ✅ | FH98 weight table (Table 2) and an independent 2.8e-6 replication. |
| Woese et al. 2000 MMBR Table 1 (polar requirement) — https://pmc.ncbi.nlm.nih.gov/articles/PMC98992/table/T1/ | ⚠️ captcha on direct fetch | PR values. |
| Novozhilov, Wolf & Koonin 2007, Biol Direct (OA) — https://pmc.ncbi.nlm.nih.gov/articles/PMC2211284/ | ✅ | Partial-optimisation reading. |
| aaRS class/subclass lists — https://encyclopedia.pub/entry/7860 ; https://aars.online/class1 ; MMBR 2003 review https://doi.org/10.1128/mmbr.67.4.550-573.2003 | ✅ | Subclass assignments used in `gc_grow3.py` [E3]. |
| Ikehara 2023, Genes 14:375 (OA) — https://pmc.ncbi.nlm.nih.gov/articles/PMC9957433/ | ✅ (Europe PMC fullTextXML) | GNC [GADV] hypothesis; states the codon–amino-acid mapping was 'accidentally selected out among the eight ways'. Copy: `notes/free_hour_2/ikehara2023.txt`. |
| Ikehara, Omori & Yoshida 2002 (GNC-SNS) — https://pubmed.ncbi.nlm.nih.gov/11956691/ | abstract ✅ | Origin of the GNC proposal. |
| Di Giulio 2008, Biol Direct 3:37 (OA) — https://doi.org/10.1186/1745-6150-3-37 | abstract via search | Extended coevolution; GNN early amino acids. |
| Biopython `ProtParamData` (KD, Hopp–Woods) and `IUPACData.protein_weights` | ✅ (biopython 1.88 in .venv) | Amino-acid property scales. |

### T06 metabolic scaling (added 2026-11-01, free session 3; E029–E038)
| Source | Status | Use |
|---|---|---|
| Clarke & Johnston 2025, BAS/UK PDC metabolic rates dataset, doi:10.5285/8d9ffd4a-16c0-4d48-9fc9-02988676ef78 (OGL) | ✅ `https://ramadda.data.bas.ac.uk/repository/entry/get/metabolic_rates.csv?entryid=synth:8d9ffd4a-16c0-4d48-9fc9-02988676ef78:L21ldGFib2xpY19yYXRlcy5jc3Y=` | 1389 rows incl. 639 mammals (with Tb) and 83 birds. Copy `notes/session_kleiber/bas_metabolic_rates.csv` (sha256 2b178f69…). Provenance of the mammal rows not stated (probably the McNab-2008-based compilation of Clarke et al. 2010; inferred). |
| AnimalTraits (Herberstein et al. 2022, Sci Data 9:265): https://raw.githubusercontent.com/animaltraits/animaltraits.github.io/main/docs/observations.csv | ✅ | Body mass + metabolic rate. **Mammal BMR largely duplicates BAS** (73/105 species identical); bird data unvetted. |
| GBIF species match API: https://api.gbif.org/v1/species/match?name=… | ✅ (slow, ~0.5 s/name) | Order/family lookup (`gbif_orders.py`). |
| Kolokotrones, Savage, Deeds & Fontana 2010, Nature 464:753 + SI — https://fontana.hms.harvard.edu/sites/fontana.hms.harvard.edu/files/documents/metabolicscaling.pdf | ✅ | Table 1 (OLS/quadratic), SI §2.2.4 PGLS (b2 0.0126 ± 0.0050), SI §3 moments derivation. Copy `notes/session_kleiber/kolokotrones2010.pdf/.txt`. |
| Clarke, Rothery & Isaac 2010, J Anim Ecol 79:610 — https://doi.org/10.1111/j.1365-2656.2010.01672.x ; NORA https://nora.nerc.ac.uk/id/eprint/9826/ | abstract ✅ (OpenAlex, NORA); full text 🔒 here: NORA record has no attached file; OpenAlex OA link onlinelibrary.wiley.com/doi/pdfdirect/… → 403 Cloudflare via curl (E035); browser not tried | 634 species/505 with Tb; quadratic; order heterogeneity. |
| White & Seymour 2003, PNAS 100:4046 — https://doi.org/10.1073/pnas.0436428100 ; PMC153045 | abstract ✅; full text 🔒 here (PMC 403, Europe PMC 500, OAI no record) | 619 species, BMR ∝ M^(2/3). |
| Dryad (Kolokotrones data; Uyeda et al.) | 🔒 API file download needs bearer token; file_stream 403 | Try again or use the Bininda-Emonds 2007 supplement / VertLife for a tree. |
| AnAge (genomics.senescence.info) | ⚠️ bot challenge on download | Not used. |
| PHYLACINE 1.2 (Faurby et al. 2018, Ecology 99:2626, doi:10.1002/ecy.2443) — mammal posterior trees `https://media.githubusercontent.com/media/MegaPast2Future/PHYLACINE_1.2/master/Data/Phylogenies/Small_phylogeny.nex` (raw.githubusercontent gives an LFS pointer) | ✅ | 1000 trees, 4253 tips; copy `notes/session_kleiber/phylacine_small.nex` (sha256 44489baaefcf49ec…). Used trees 0–19 (E032) / 0–2 (E033–E034) for PGLS. |
| PHYLACINE 1.2 synonymy table — `https://raw.githubusercontent.com/MegaPast2Future/PHYLACINE_1.2/master/Data/Taxonomy/Synonymy_table_with_unaccepted_species.csv` | ✅ | Name resolution (590/636 BAS species), Order.1.2, Bases (sequence data flag). Copy `phylacine_synonyms.csv` (sha256 c50fc8d33c5b22d5…). |
| Springer Link article pages (e.g. Yarus, Widmann & Knight 2009 JME, doi:10.1007/s00239-009-9270-1) | ⚠️ curl gets a JS "Client Challenge" page; ✅ WebFetch works (2026-11-01) | Tables render cleanly at `https://link.springer.com/article/<doi>/tables/<n>` via WebFetch (the article page shows only "Full size table"). WebFetch of `/content/pdf/<doi>.pdf` returns the text, but tables come out garbled and the in-article sequence lists did not appear. Transcribed Table 1: `notes/session_yarus/table1.tsv` (E040). |
| NCBI Bookshelf (e.g. NBK6584, Knight, Landweber & Yarus "Tests of a Stereochemical Genetic Code") | ⚠️ WebFetch 403; curl gets a reCAPTCHA page (2026-11-01) | Only search-engine extractions were seen (E040). Open it in a browser if the chapter's date or dataset matters. |

## Earth, climate, and society
| Source | Status | Use |
|---|---|---|
| NASA GISTEMP: https://data.giss.nasa.gov/gistemp/tabledata_v4/GLB.Ts+dSST.csv | ✅ | Global temperature anomaly CSV. |
| NOAA Mauna Loa CO₂: https://gml.noaa.gov/webdata/ccgg/trends/co2/co2_mm_mlo.txt | ✅ | |
| USGS earthquakes (FDSN): https://earthquake.usgs.gov/fdsnws/event/1/ | ✅ | `query?format=csv&starttime=…&minmagnitude=…` |
| NOAA NCEI https://www.ncei.noaa.gov · IPCC reports https://www.ipcc.ch/reports/ | ✅ | |
| Our World in Data: https://ourworldindata.org | ✅ | Any chart: append `.csv`, e.g. `…/grapher/life-expectancy.csv`. |
| World Bank API: https://api.worldbank.org/v2 | ✅ | `…/country/US/indicator/SP.POP.TOTL?format=json` |
| FRED: https://fred.stlouisfed.org | ⏳ timed out | Retry later. |

## General knowledge graphs, texts, and data
| Source | Status | Use |
|---|---|---|
| Wikidata SPARQL: https://query.wikidata.org/sparql | ✅ | `curl -G --data-urlencode 'query=SELECT …' -d format=json https://query.wikidata.org/sparql`. Treat it as retrieved information, not ground truth. |
| Wikipedia API: https://en.wikipedia.org/w/api.php | ✅ | Use it for orientation only, then follow its citations. |
| Internet Archive: https://archive.org/advancedsearch.php · Project Gutenberg: https://www.gutenberg.org | ✅ | Historical primary texts. |
| SNAP networks https://snap.stanford.edu/data/ · Network Repository https://networkrepository.com · UCI ML repo https://archive.ics.uci.edu · Hugging Face datasets https://huggingface.co/datasets | ✅ | Data for complex-systems work. |
| BIPM (SI units): https://www.bipm.org | ✅ | |
| Complexity Explorables: https://www.complexity-explorables.org | ✅ | Interactive models; good for building intuition only. |
