# Dual-valued Boolean datapaths

Recorded numerical results accompanying **Dual-Valued Boolean Datapaths for Single-Pass Input-to-Node Structural Sensitivity**.

Authors: Joao Vitor Mattos Scarpate; Leandro Rodrigues da Silva Souza; Geraldo Andrade de Oliveira.

Corresponding author: Joao Vitor Mattos Scarpate, IFES Campus Serra. ORCID: [0009-0000-2114-1679](https://orcid.org/0009-0000-2114-1679). Email: joaovitorscarpate@gmail.com.

## Scope

The manuscript defines a Boolean signal value paired with a vector of input-direction sensitivities. Gate-local propagation computes an input-to-node structural quantity in a single topological traversal. Agreement with the functional Boolean derivative is proved under directional independence. In general reconvergent circuits there is no universal equality, upper-bound, or lower-bound guarantee.

This deposit preserves the existing numerical output files without rerunning experiments. It contains recorded results, including aggregate statistics, rather than a complete collection of per-input execution traces. Experiment-generation scripts are not part of this deposit.

## Files and correspondence to the manuscript

| File | Contents | Manuscript correspondence |
| --- | --- | --- |
| `E3_results.csv` | 16 recorded sensitivity comparisons for four analytical expressions | Experiment 3, reconvergence table and analytical discussion |
| `simulation_results.json` | c17 agreement counts and eight scalability configurations | Experiments 4–6, scalability table and cost/runtime plots |
| `iscas85_results.csv` | Aggregate results for 11 mapped ISCAS-85 circuits | Experiment 7, benchmark table and reconvergence/speedup/overhead figures |
| `CITATION.cff`, `CITATION.bib` | Dataset citation metadata | Citation of this deposit |
| `submission/` | Manuscript, source figures, cover letter, highlights, presentation and editorial materials | Journal submission package |

Experiments 1 and 2 are represented by their existing manuscript figures. Their individual numerical records are not included in these three result files.

## Data dictionary

### ISCAS-85 results

One row corresponds to one mapped benchmark circuit.

| Column | Meaning |
| --- | --- |
| `Circuit` | Benchmark identifier |
| `N_in` | Number of primary inputs |
| `Gates` | Gate count of the evaluated mapped netlist |
| `Match%` | Percentage of input-vector/output pairs whose complete structural and functional sensitivity vectors are equal |
| `Overest%` | Percentage for which the structural vector contains every functional sensitivity bit, including equality; an inclusion rate |
| `Reconv%` | Structural reconvergence metric reported for the evaluated netlist, in percent |
| `Area_OH%` | Equivalent gate-count overhead of the dual representation, in percent; not measured silicon area |
| `Time_Dual_ms` | Mean software time per input vector for dual propagation, in milliseconds |
| `Time_FD_ms` | Mean software time per input vector for finite-difference enumeration, in milliseconds |
| `Speedup` | Reported finite-difference/dual runtime ratio; rounded values may differ slightly from a ratio computed from the displayed times |

The Python implementation uses bitmasks. Circuits with at most 10 inputs were evaluated exhaustively; larger circuits used 1,000 random input vectors. A high speedup does not establish functional agreement. `Overest%` below 100 indicates comparisons with omitted functional sensitivity bits. It is not a count of strictly overestimated bits.

### c17 and scalability results

`simulation_results.json` contains `c17` and `Scaling`.

- `c17.TotalChecks`: 64 complete-vector comparisons, from 32 input vectors and two outputs.
- `c17.TotalMatches`: 56 equal-vector comparisons.
- `c17.MatchRate`: agreement percentage, 87.5.
- `Scaling[].N`: primary-input count (4, 8, ..., 32).
- `NominalArea`, `DualArea`: equivalent gate counts for the original and dual representations.
- `DualTime`, `FDTime`: mean wall-clock milliseconds per input vector.
- `MatchRate`: percentage of equal individual sensitivity components across 100N comparisons. This is different from the complete-vector ISCAS-85 Match metric.

One random circuit with 8N gates and one output was used per input width. The last generated gate is the output. Reuse of existing signals permits reconvergence. Timing used separate batches of 100 random vectors. Both timers include input-vector generation. Here `FDTime` includes the full FD-based validation procedure, including an additional dual evaluation and agreement checks; it is not an isolated FD runtime. This differs from the Python ISCAS-85 timing procedure.

### Reconvergence examples

`E3_results.csv` preserves the recorded comparison rows. `Circuit` and `Variable` identify the expression and direction; `S_struct` and `S_func` are the structural and functional bits; `Match` records equality; `Class` identifies cancellation, redundancy or reconvergence. The original file does not include explicit input-vector columns, so repeated rows must not be treated as duplicate records to discard. The final reconvergent row records structural 0 versus functional 1.

## Citation and availability

Use the root `CITATION.cff` (GitHub “Cite this repository”) or `CITATION.bib`. The manuscript cites this repository as a dataset. The manuscript has no publication DOI yet. Repository version 1.0.0 identifies this prepared deposit; it is not an assertion that a journal article has been published.
