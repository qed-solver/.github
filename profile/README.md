# QED, the Query Equivalence Decider/Determinator

## Overview

The QED project aims to resolve SQL query equivalence efficiently. It has three parts:

- A SQL parser that compiles SQL queries to intermediate representations for the prover and disprover.
- A prover that validates the equivalence of queries. The prover may produce false negative results, where the queries are equivalent but the prover cannot prove it.
- A disprover that searches for database instances where the queries produce different results. The disprover may produce false positive results, where the queries are inequivalent but the disprover cannot find a database instance that distinguish the queries.

## Usage

The workflow of the project starts from the parser and ends in the prover and disprover. Currently the parser and the prover have been packaged with `Nix`, so they can be easily use like this:

```sh
# Please have Nix installed in your system with experimental features enabled.
# Now we enter a shell with the parser and the prover.
# Please allow the use of Cachix to accelerate your experience.
nix shell github:qed-solver/parser github:qed-solver/prover

# Assume that we have an example.sql that contains
# table schema definitions and two SQL queries.
# The parser generates example.json and example.rkt in the same directory.
# example.json is for the prover and example.rkt is for the disprover.
qed-parser example.sql

# We run the prover to verify the equivalence.
# The results are printed on stdout.
# The prover also generates example.res:
# the first line logs whether the equivalence is provable,
# the second line logs the time spent by the prover.
qed-prover example.json
```

Please refer to the READMEs in the repositories within this project for more details.
