# Debugging symbols
- `-g0` - No debugging symbols
- `-g2` - Maximum debugging symbols

# Optimisation
`-O0` - No compiler optimisations
`-O3` - Maximum compiler optimisations
`-flto` - Enable link time optimisations

# Static analysis
Enable lots of good warnings, and treat them as errors so that they get fixed.

- `-Wall`
- `-Wextra`
- `-Wshadow`
- `-Wconversion`
- `-Wpedantic`
- `-Werror`

Static analysers
- `-fanalyzer`
- cppcheck
- clang-tidy

# References
- [cpp-weekly][1]

[1]: https://github.com/lefticus/cpp_weekly/issues/175