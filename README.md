This repository contains the encoding circuits, worked examples and MATLAB source code that accompany the paper
**"Fault-Tolerant Encoding of Entanglement-Assisted Quasi-Cyclic  QLDPC codes over Qudits"**.

The code constructs, verifies and draws the encoding circuits of **Fault-Tolerant Encoding of Entanglement-Assisted Quasi-Cyclic  QLDPC codes over Qudits** $\mathbb{F}_p$ in four ways:

| Method | Description |
|---|---|
| **Proposed** | the proposed encoding strategy (Steps 1–5, decoder $\mathcal{D}=U_H U_4 U_3 U_2 U_1$, encoder $\mathcal{E}=\mathcal{D}^\dagger$) |
| **Proposed + Beam** | the proposed encoder after beam-search optimisation of its ADD gates |
| **NG** | the encoder of P. J. Nadkarni and S. S. Garani, *IEEE Trans. Quantum Eng.*, vol. 2, 2021 (Algorithm 2) |
| **NG + Beam** | the NG encoder after beam-search optimisation of its ADD gates |

The beam search follows A. Sodhani, P. Kumar, S. S. Garani and K. K. Parhi, *"Optimizing encoder circuits of
entanglement-assisted quantum LDPC codes via beam search,"* IEEE TCAS-II, vol. 73, no. 11, 2026,
**extended here from GF(2) to GF(p)**.

---

## Repository contents

```
.
├── EA-QCQLDPC-Encoder-BeamSearch-MATLAB/      MATLAB code: Proposed and Proposed + Beam encoders
├── EA-QCQLDPC-NG-Encoder-BeamSearch-MATLAB/   MATLAB code: NG and NG + Beam encoders
├── Examples for Circuits.pdf                  the examples (codes, parity-check matrices, parameters)
├── all_circuits_examples_1_10.pdf             encoding circuits of Examples 1-10 for all four methods
└── README.md
```

* **`Examples for Circuits.pdf`** – the ten example codes: field $\mathbb{F}_q$, circulant size $r$, $P(0)$, the
  parity-check matrices $H_1$, $H_2$, their ranks, $\mathrm{rank}(H_1H_2^T)$ and the code parameters.
* **`all_circuits_examples_1_10.pdf`** – 40 encoding circuits (4 methods × 10 examples), one per page, each with
  its gate counts (ADD, MUL, DFT, SWAP) and two-qudit depth.
* **MATLAB folders** – self-contained programs (one `.m` file each, no toolboxes required) that build the
  encoder of an example, verify it, print the gate counts and the gate sequence, and draw the circuit.

---

## The examples

All codes are EA-QC-QLDPC codes with a single e-dit ($c=1$), obtained from
$H_1$, $H_2$ built from $P(0)=\mathrm{diag}\{a_0,\dots,a_{r-1}\}$ and its shifts $P(i)$
(each row of $P(0)$ cyclically shifted $i$ positions to the right, i.e. $P(i)=P(0)S^{i}$ with $S$ the right
circulant permutation matrix).

| Ex. | Code | $\ell_1$ | $\ell_2$ | $d$ |
|---|---|---|---|---|
| 1 | $[[25,16;1]]_3$ | 1 | 1 | 2 |
| 2 | $[[25,12;1]]_3$ | 1 | 2 | 2 |
| 3 | $[[25,8;1]]_3$ | 2 | 2 | 4 |
| 4 | $[[25,4;1]]_3$ | 2 | 3 | 4 |
| 5 | $[[49,36;1]]_3$ | 1 | 1 | 2 |
| 6 | $[[49,30;1]]_3$ | 1 | 2 | 2 |
| 7 | $[[49,24;1]]_3$ | 2 | 2 | 4 |
| 8 | $[[49,18;1]]_3$ | 2 | 3 | 4 |
| 9 | $[[49,12;1]]_3$ | 3 | 3 | 6 |
| 10 | $[[9,4;1]]_5$ | 1 | 1 | 2 |

### Gate counts of the encoders

ADD = number of two-qudit ADD/ADD$^\dagger$ gates; Total = ADD + MUL + DFT (+ SWAP).

| Ex. | Code | Proposed ADD (Total) | Proposed + Beam ADD (Total) | NG ADD (Total) | NG + Beam ADD (Total) |
|---|---|---|---|---|---|
| 1 | $[[25,16;1]]_3$ | 59 (122) | 45 (68) | 52 (129) | 42 (47) |
| 2 | $[[25,12;1]]_3$ | 94 (197) | 67 (90) | 76 (184) | 66 (72) |
| 3 | $[[25,8;1]]_3$ | 126 (208) | 87 (101) | 119 (255) | 81 (89) |
| 4 | $[[25,4;1]]_3$ | 102 (177) | 68 (81) | 103 (232) | 86 (99) |
| 5 | $[[49,36;1]]_3$ | 125 (256) | 91 (138) | 114 (278) | 105 (197)* |
| 6 | $[[49,30;1]]_3$ | 249 (508) | 127 (174) | 198 (461) | 174 (181) |
| 7 | $[[49,24;1]]_3$ | 357 (566) | 255 (282) | 293 (627) | 205 (217) |
| 8 | $[[49,18;1]]_3$ | 420 (701) | 220 (247) | 350 (748) | 285 (301) |
| 9 | $[[49,12;1]]_3$ | 375 (584) | 226 (259) | 514 (1064) | 298 (318) |
| 10 | $[[9,4;1]]_5$ | 17 (36) | 15 (24) | 15 (43) | 20 (24) |

\* one block of the NG encoder could not be decomposed within the tested beam widths and was kept unchanged.
The NG counts include SWAP gates (Examples 1, 2, 4, 5, 6, 8, 9, 10). Beam-search results depend on the beam
widths tried; the MATLAB code may give slightly different (typically fewer) MUL counts because it prefers
multipliers $\lambda=\pm 1$ when candidates are tied.

---

## Running the MATLAB code

Requirements: MATLAB R2016b or newer (no toolboxes). Each program is a single self-contained file; the file
name must match the function name on its first line.

```matlab
% Proposed and Proposed + Beam
>> cd EA-QCQLDPC-Encoder-BeamSearch-MATLAB
>> run_example_9_4_F5_proposed_beam

% NG and NG + Beam
>> cd EA-QCQLDPC-NG-Encoder-BeamSearch-MATLAB
>> run_example_9_4_F5_NG_beam
```

### Input

The example is specified by a few lines at the top of each file (shown for Example 10, $[[9,4;1]]_5$):

```matlab
p  = 5;                   % field F_p (p prime)
r  = 3;                   % circulant size
a  = [1 2 4];             % diagonal of P(0)
E1 = [0 2 1];             % H1 = [P(0) P(2) P(1)]   (one row per block-row)
E2 = [0 1 2];             % H2 = [P(0) P(1) P(2)]
SHIFT  = 'row';           % P(i) = P(0) S^i  (each row of P(0) shifted i positions to the right)
WIDTHS = [1 10 50];       % beam widths for the beam-search optimisation
TCAP   = 120;             % time cap (s) per beam run
```

Each row of `E1`/`E2` lists the exponents of one block-row, e.g.
$H_2=\begin{bmatrix}P(0)&P(3)&P(4)&P(2)&P(1)\\P(0)&P(4)&P(2)&P(1)&P(3)\end{bmatrix}$ is
`E2 = [0 3 4 2 1; 0 4 2 1 3]`. To run another example, change only these lines.

### Output

* $P(i)$, $H_1$, $H_2$, $\mathrm{rank}(H_1)$, $\mathrm{rank}(H_2)$, $\mathrm{rank}(H_1H_2^T)$ and the code parameters;
* the extended stabilizer matrices $[H_1\,|\,-D_x]$, $[H_2\,|\,D_z]$ after Gaussian elimination and column reordering;
* the encoder before and after beam-search optimisation: gate counts (ADD, MUL, DFT, SWAP, total, two-qudit depth),
  the reduction of two-qudit gates, and the complete gate sequence;
* the circuits as PDF files (e.g. `ex_9_4_F5_proposed.pdf`, `ex_9_4_F5_proposed_beam.pdf`).

Expected result for Example 10, $[[9,4;1]]_5$:

| Encoder | ADD | MUL | DFT | SWAP | Total | Two-qudit depth |
|---|---|---|---|---|---|---|
| Proposed | 17 | 17 | 2 | 0 | 36 | 10 |
| Proposed + Beam | 15 | 7 | 2 | 0 | 24 | 11 |
| NG | 15 | 24 | 2 | 2 | 43 | 10 |
| NG + Beam | 20 | 2 | 2 | 0 | 24 | 14 |

### Verification

Every encoder (before and after optimisation) is verified by **stabilizer-tableau simulation over
$\mathbb{F}_p$**: the program checks that the encoder maps the stabilizers of the input state
$|0\rangle^{\otimes a}|\psi\rangle|\Phi\rangle$ onto the full extended stabilizer group of the code,
including the receiver half of the e-dit. The program stops with an error if a check fails.

---

## Conventions

* **Qudits.** Qudits $1,\dots,n$ are at the transmitter (the transmitter half of the e-dit is qudit $n$);
  qudit $n+1$ is the receiver half of the e-dit and is never acted on by the encoder.
  The columns of $H_1$, $H_2$ are reordered (X-pivots, Z-type ancillas, information qudits, e-dit);
  the order is printed by the programs.
* **Proposed encoder:** ancillas first, information qudits next. **NG encoder:** information qudits first,
  ancillas next.
* **E-dit.** $|\Phi\rangle=\frac{1}{\sqrt{p}}\sum_{x\in\mathbb{F}_p}|-x\rangle|x\rangle$
  (identical to $|\eta\rangle=\frac{1}{\sqrt{p}}\sum_g|g,-g\rangle$ of Nadkarni and Garani), stabilized by
  $X(x)\otimes X(-x)$ and $Z\otimes Z$.
* **Gates** (rows `[type a b v]` in the code):

  | Gate | Action | In the circuits |
  |---|---|---|
  | ADD$(a\to b)$ | $\lvert x\rangle_a\lvert y\rangle_b\mapsto\lvert x\rangle_a\lvert y+x\rangle_b$ | control dot, box `+` |
  | ADD$^\dagger(a\to b)$ | $\lvert x\rangle_a\lvert y\rangle_b\mapsto\lvert x\rangle_a\lvert y-x\rangle_b$ | control dot, box `-` |
  | $M_\gamma$ | $\lvert x\rangle\mapsto\lvert\gamma x\rangle$ | box `Mγ` |
  | $F$, $F^\dagger$ | DFT and inverse DFT | box `F`, `F*` (or $F^\dagger$) |
  | SWAP | exchanges two qudits | ×–× |

  A scaled addition $\mathrm{ADD}_\lambda$ ($\lambda\neq\pm1$) is realised as $M_{\lambda^{-1}}\,\mathrm{ADD}\,M_\lambda$.
* **Depth** is the ASAP two-qudit (ADD/SWAP) depth.

### Beam-search optimisation (extension to GF(p))

With the DFT gates held fixed, the ADD, MUL and SWAP gates of the encoder realise a linear map
$|\mathbf v\rangle\mapsto|A\mathbf v\rangle$ with $A\in GL(n+1,\mathbb{F}_p)$. The beam search applies row
operations $R_i\leftarrow R_i+\lambda R_j$ ($\lambda\in\mathbb{F}_p^*$), ranked by the number of nonzero
off-diagonal entries, until $A$ is diagonal; the diagonal is realised by MUL gates. The search depth is bounded
by the original two-qudit gate count, duplicate states are merged, and ties are broken deterministically
(preferring $\lambda=\pm1$). The method is heuristic and does not guarantee a minimum gate count.

---

## Citation

* P. J. Nadkarni and S. S. Garani, "Encoding of nonbinary entanglement-unassisted and assisted stabilizer codes,"
  *IEEE Trans. Quantum Eng.*, vol. 2, pp. 1–22, 2021.
* A. Sodhani, P. Kumar, S. S. Garani and K. K. Parhi, "Optimizing encoder circuits of entanglement-assisted
  quantum LDPC codes via beam search," *IEEE Trans. Circuits Syst. II: Express Briefs*, vol. 73, no. 11,
  pp. 1159–1163, 2026.
