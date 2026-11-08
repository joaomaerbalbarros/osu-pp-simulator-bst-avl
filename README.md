# Trees in the Real World: osu! plays in a BST and an AVL tree

Assignment for the Algorithms and Data Structures course (UFTM).
Author: João Maerbal Nunes Barros.

The program loads the 200 top plays of an osu! profile into a Binary Search
Tree (BST) and an AVL tree, keyed by beatmap ID. It supports inserting,
searching and removing plays, the three traversals, a pp simulator for a new
play and a performance comparison between the two trees.

Presentation video (in Portuguese): https://www.youtube.com/watch?v=bza74MyH1AQ

## Build and run

Requires only `gcc` and the C standard library. Run it from this folder,
because the program reads `jogadas_osu.csv` from the current directory.

```bash
gcc -fsanitize=address -g -Wall -o trabalho trabalho.c
./trabalho
```

The menu (in Portuguese) offers:

1. Insert a play
2. Search a play by ID
3. Remove a play by ID
4. Traversals (in-order, pre-order, post-order)
5. Tree heights
6. Simulate a play worth x pp
7. Comparison experiment

## pp simulator

Given a new play worth `x` pp, the program counts how many plays in the tree
have at least `x` pp to find the position `n` the new play would take in the
profile, then applies osu!'s position weight: `x · 0.95^(n−1)`. Since the
tree is ordered by beatmap ID and not by pp, every node has to be visited.

## Experiment results

| Scenario | Tree | Height | Comparisons (total) | Comparisons (average) |
|---|---|---|---|---|
| A: file order | BST | 17 | 1888 | 9.44 |
| A: file order | AVL | 9 | 1368 | 6.84 |
| B: IDs in ascending order | BST | 200 | 20100 | 100.50 |
| B: IDs in ascending order | AVL | 8 | 1353 | 6.76 |

In scenario B the BST degenerates into a linked list, while the AVL tree keeps
a logarithmic height. The full analysis is in the report.

## Data

`jogadas_osu.csv` holds the 200 plays from the Best Performance section of
the profile https://osu.ppy.sh/users/13699780, collected on 2026-10-14 through
the official osu! API. The columns are beatmap name, beatmap ID, pp (3 decimal
places) and date, separated by `;` and in chronological order.

The script `scripts/coletar_jogadas.py` regenerates the file. The data changes
whenever the player sets new plays; the CSV in this repository is the one used
for the results above.

## Layout

The code, report and documentation are in Portuguese.

| Path | Contents |
|---|---|
| `trabalho.c` | the program |
| `jogadas_osu.csv` | the data |
| `docs/relatorio.pdf` | submitted report |
| `docs/enunciado.pdf` | assignment statement |
| `docs/TRABALHO.md` | proposal, technical decisions and stage plan |
| `docs/REFORMULACAO_14-10.md` | changes agreed with the professor on 2026-10-14 (key = ID) |
| `docs/DIARIO.md` | development log: bugs found and how they were fixed |
| `docs/REVISAO_CODIGO.md` | line-by-line code review |
| `docs/ROTEIRO_VIDEO.md` | video script |
| `scripts/` | data collection script |

## Use of AI

Development was assisted by AI (Claude, by Anthropic), as allowed by the
professor and declared in the report. Commits made with this assistance carry
the `Co-Authored-By: Claude` trailer.
