# rstyles 0.7.3 (3.12.2024)

## Enhancements

- `make_scoring_matrix_aem()` has a new argument `eType` allowing to prepare scoring matrices with distnict processes regarding the *extremity* trait in different nodes of the decision tree, as desribed in (Merhof & Meiser, 2023).

# rstyles 0.7.2 (1.07.2024)

## Bug fixes

- `make_mplus_irtree_model_syntax()` and `make_mplus_gpcm_model_syntax()` collapses ANALYSIS element to be a single string what makes `MplusAutomation::mplusModeler()` not failing when run in R >=4.3.0.

# rstyles 0.7.1 (9.02.2023)

## Bug fixes

- `make_mplus_irtree_model_syntax()` and `make_mplus_gpcm_model_syntax()` works with `items` provided as a simple character vector.

# rstyles 0.7.0 (9.02.2023)

## New features

- New functions `make_mplus_irtree_model_syntax()` and `make_mplus_gpcm_model_syntax()` enabling to conveniently prepare the Mplus syntax specifying response-style models.
- New function `read_mplus_object_results()` enabling convenient reading results from an estimated *mplusObject*.

## Bug fixes

- `expand_responses()` deals with data with responses being a *tibble*.
- `generate_intercepts_sqn()` and thus `generate_intercepts()` accepts `argsd` containing elements that are not atomic vectors, e.g. list of matrices.

## Other changes

- Considering remarks of Plieninger (2020) regarding the interpretation of IRTree models the distinction between *sequential* and *simultaneous* response processes was (almost completely) removed from the package parameter names and descriptions in documentation in favor of labeling them as *IRTree* and *GPCM*.

# rstyles 0.6.0 (23.12.2021)

## New features

- New functions `make_scoring_matrix_rt()` and `make_scoring_matrix_stz()` enabling convenient construction of scoring matrices using *random thresholds* and *sum to zero* approaches.

# rstyles 0.5.0 (20.12.2021)

## New features

- New function `generate_item_expected_scores()` that allows to generate (by numerical integration) expected probabilities of responses (response categories) given an item object or test object and covariance matrix of latent traits.
  - Dependency from the package *mvtnorm* was added to be able to compute weights for quadrature points.
- New utility functions `thresholds2intercepts()` and `intercepts2thresholds()` allowing conversion between *thresholds* and *intercepts* parameterizations of GPCM items.

## Bug fixes

- `expand_responses()` do not take into account missing values in the data while performing assertion that all values in the data are members of the set of values defined by rownames of the `scoringMatrix`.
- `generate_intercepts()` correctly transforms parameters generated in a parameterization involving item difficulty and thresholds relative to his difficulty into parametrization of intercepts in case of GPCM items (i.e. it cumulatively sums up thresholds and subtracts difficulty instead of adding difficulty to thresholds).
  - Documentation was corrected to explain, that in case of GPCM mode arguments define how values of *thresholds* should be generated but that function returns accordingly computed *intercepts*.

## Other changes

- `make_item()` allows to get non-zero first element of the `intercepts` argument if length of `intercepts` equals to the number of rows of the `scoringMatrix` (previously it returned an error), but still warns that this is atypical specification.

## Internals

- Test where updated to work correctly after the changes in `generate_intercepts()`.

# rstyles 0.4.0 (21.07.2021)

## New features

- `make_test()` assigns names to the created items by default and provides additional `names` argument if user wants to provide names himself/herself.
- `generate_test_responses()` uses items' names (if there are any) to name columns of the returned matrix.
- `generate_test_responses()` converts matrix it returns to numeric one (if only this is possible without loss of information); it also provides additional argument `tryConvertToNumeric` that allows to bring back its former behavior (i.e. returning a character matrix).
- `generate_intercepts_sml()`, and consequently `generate_intercepts()` when called with `FUNt` argument, returns intercepts matrix with additional first columns of zeros to make it compatible with the format that uses function `simdata()` from *mirt* package (`generate_test_responses()` was, and still is, able to deal with providing it intercepts either with or without such additional zeros).

## Documentation

- Additional section in README.md describing the way function `simdata()` from package *mirt* may be used to speed up generation of GPCM responses.
- Some improvements in documentation.

# rstyles 0.3.0 (5.05.2021)

## New features

- Functions that enables user to generate *items* and *tests*: `generate_slopes()`, `generate_intercepts()` and `make_test()`.
- Functions to compute log-normal distribution parameters on the scale of the actual variable (i.e. the exponential scale): `lnorm_mean()`, `lnorm_sd()` and `find_pars_lnorm()`.
- Function that enables user to generate a very simple *scoring matrix* that doesn't deal with any response styles: `make_scoring_matrix_trivial()`. It is useful if one wants to use *rstyles* for simulations that don't involve response styles.

## Bug-fixes

- Some improvements in documentation.

# rstyles 0.2.0 (17.12.2020)

- First ready to use version of the package.
