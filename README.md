# _k_-SatLib

_k_-SatLib is a library of uniform random Boolean Satisfiability (SAT or _k_-SAT) problems for evaluating SAT solvers. This library is provided as is under the GNU V3.0 license and is free for use, modification, and distribution for all applications. If you use this library in your research or publication please cite this repository. It is our hope that this library can be used to provide points of comparison between newly developed SAT solvers capable of supporting problems of _k_ > 3. All problem instances are provided as ".cnf" files in the [DIMACS](https://jix.github.io/varisat/manual/0.2.0/formats/dimacs.html) format.

## Dataset Generation
The datasets provided were generated using the [_k_-SatGen](https://github.com/mixedsignal-umich/k-SatGen) MATLAB script. This script is capable of forced (satisfiable only) or unforced generation of instances. Forced instances are saved with a "f_" prefix and unforced instances are saved with a "uf_" prefix. For forced generation a solution is randomly generated and all clauses are generated to satisfy this planted solution. These problems are typically easier than unforced problems of the same dimension, but are faster to generate. The unforced generation is performed in the same manner as that of SATLIB[^1] where clauses are randomly generated without any planted solution and may result in either a satisfiable (SAT) or unsatisfiable (UNSAT) problem. During unforced generation, if a clause is created with multiple of the same variable/literal it is filtered out and discarded. All generated problems are verified as satisfiable or unsatisfiable with the [CaDiCal](https://github.com/arminbiere/cadical) solver[^2].

All datasets are generated at the phase transition clause-to-variable ratio where the most challenging instances exist. For the 3-SAT instances the same ratios as used in the SATLIB unforced [library](https://www.cs.ubc.ca/~hoos/SATLIB/benchm.html) are used when possible. For other problem sizes the established ratio of 4.26[^3] is used as a starting point. While the established phase transition ratios hold for large numbers of variables, smaller problems often require a larger ratio to achieve the same level of difficulty. When generating smaller unforced problems, we attempt set the ratio such that half of the problems generated are satisfiable and half are unsatisfiable. The ratios for the unforced k = 3 data sets are reported below. The ratios for each unforced problem set are reported in their respective directories. For k = 4 - 10 the ratios from _Information, Physics, and Computation_[^4] were used with minor adjustments made as necessary for smaller problems.

## Dataset Details
Each dataset contains 1000 problem instances. During generation it is possible that more than 1000 instances will be generated due to the multi-threaded operation of _k_-SatGen and the random nature of unforced generation. In these cases only the first 1000 problems are saved and the rest are discarded.

#### Metrics for the uf_*_k3 Dataset and Comparison with SATLIB
| Variables (n) | Clauses (m) | Clause:Variable Ratio | SAT Problems | UNSAT Problems | k-SatLib SAT TTS* | SATLIB SAT TTS* | k-SatLib UNSAT TTS* | SATLIB UNSAT TTS* |
| :------------ | :---------- | :-------------------: | :----------: | :------------: | ----------------: | --------------: | ------------------: | ----------------: |
| 20            | 91          | 4.55                  | 1146         | 1002           |                   |                 |                     |                   |
| 50            | 218         | 4.36                  | 1035         | 1005           |                   |                 |                     |                   |
| 75            | 325         | 4.33                  | 1005         | 1131           |                   |                 |                     |                   |
| 100           | 430         | 4.30                  | 1004         | 1084           |                   |                 |                     |                   |
| 125           | 538         | 4.30                  | 1010         | 1186           |                   |                 |                     |                   |
| 150           | 645         | 4.30                  | 1011         | 1293           |                   |                 |                     |                   |
| 175           | 753         | 4.30                  | 1012         | 1436           |                   |                 |                     |                   |
| 200           | 860         | 4.30                  | 1006         | 1478           |                   |                 |                     |                   |
| 225           | 960         | 4.27                  | 1007         | 1117           |                   |                 |                     |                   |
| 250           | 1065        | 4.26                  | 1042         | 1010           |                   |                 |                     |                   |
###### *Time-to-Solution (TTS) measured by evaluating each dataset with CaDiCaL[^2] 100 times and taking the mean TTS for each problem. The evaluation was performed on an Apple M3 Pro 12-Core CPU.

## References
[^1]: Hoos, H. H., & Stützle, T. (2000). SATLIB: An online resource for research on SAT. Sat, 2000, 283-292.
[^2]: Biere, A., Faller, T., Fazekas, K., Fleury, M., Froleyks, N., & Pollitt, F. (2024, July). CaDiCaL 2.0. In International Conference on Computer Aided Verification (pp. 133-152). Cham: Springer Nature Switzerland.
[^3]: Mézard, M., Parisi, G., & Zecchina, R. (2002). Analytic and algorithmic solution of random satisfiability problems. Science, 297(5582), 812-815.
[^4]: Mezard, M., & Montanari, A. (2009). Information, physics, and computation. Oxford University Press.
