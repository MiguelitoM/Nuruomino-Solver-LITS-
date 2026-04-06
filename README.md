# NURUOMINO Solver (LITS Puzzle)

## Overview

This project implements a constraint-based solver for the NURUOMINO (LITS) puzzle, developed for the Artificial Intelligence course at Instituto Superior Técnico.

The solver models the puzzle as a search problem and explores the solution space by incrementally assigning tetrominoes to regions while enforcing all structural constraints of the puzzle.

## Problem Description

The board is an N×N grid partitioned into regions. The objective is to assign exactly one tetromino (L, I, T, or S) to each region such that:

- No two identical tetrominoes are orthogonally adjacent (considering rotations and reflections as equivalent)
- All filled cells form a single connected component (orthogonal connectivity)
- No 2×2 fully filled subgrid exists

This combination of global and local constraints makes the problem highly combinatorial and suitable for AI search techniques.

## Modeling

The problem is modeled as a classical search problem:

- **State**: partial assignment of tetrominoes to regions
- **Action**: placement of a tetromino (type + orientation) in a specific region
- **Goal**: all regions filled with a valid configuration satisfying all constraints

The board is represented internally with support for:
- region adjacency queries
- cell adjacency (including diagonals)
- validation of local and global constraints

## Constraint Handling

Constraint validation is applied incrementally during the search:

- **Local constraints**
  - valid placement inside region boundaries
  - no overlap with existing assignments

- **Adjacency constraints**
  - prevent identical tetrominoes from touching orthogonally

- **Global constraints**
  - maintain connectivity of filled cells
  - detect and prevent 2×2 filled blocks early

Invalid states are pruned immediately to reduce the search space.

## Search Strategy

The solver is compatible with different search strategies provided in the course framework, including:

- Depth-First Search (DFS)
- Greedy Search
- A*

Performance depends heavily on:
- early constraint pruning
- ordering of region assignments
- heuristic design (when applicable)

## Input / Output

The program reads a puzzle instance from standard input, where each cell contains the identifier of its region.

The output is a solved grid where each placed tetromino is represented by its corresponding letter (**L**, **I**, **T**, or **S**).

## Running

Run the solver with:

```bash
python3 nuruomino.py < sample-nuruominoboards/test01.txt
