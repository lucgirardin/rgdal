# rgdal

This is a fork of the retired **RGDAL** package to make it compatible with recent versions of R (currently 4.6.1 and later).

The original `rgdal` package was retired from CRAN in 2023. This fork fixes compilation errors that arise when building against newer versions of R, primarily caused by macro conflicts between R's `length` macro and C++ standard library methods.

## Installation

Install directly from GitHub:

```r
remotes::install_github("lucgirardin/rgdal")
```

## Changes

The following fixes were applied to resolve compilation errors with R 4.6.1:

- **`length` macro conflict**: R defines a `length()` macro that conflicts with C++ `std::string::length()` and similar calls. Fixed by adding `#undef length` after R headers and replacing bare `length()` calls with `Rf_length()` where appropriate.
- **GDAL API changes**: `GetMetadata()` now returns `CSLConstList` (`const char *const *`); updated variable types accordingly.
- **OGR API changes**: `GetSpatialRef()` now returns `const OGRSpatialReference *`; fixed by cloning the returned SRS via `Clone()` and properly deleting it.

## References

- Original package: <https://cran.r-project.org/package=rgdal>
- Upstream repository: <https://github.com/cran/rgdal>
