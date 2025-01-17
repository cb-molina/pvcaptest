# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[0.10.0]: https://github.com/pvcaptest/pvcaptest/compare/v0.9.0...v0.10.0
## [0.10.0] - 2021-07-25
### Added
- Added the filter_missing CapData method to remove missing data from specified columns.
By default removes only intervals that contain missing data in the regression variable
columns.
- Added option to filter_irr method to specify using the reporting irradiance in the CapData object as the
reference irradiance.
- Added option to the filter_time method to drop the specified time period instead of dropping all other times.
- Added option to filter_clearsky method to keep time periods with unstable irradiance.
- Added new attributes to CapData: removed, kept, filter_counts. The update_summary decorator now stores the
index of points removed, the index of points remaining after each filter, and the number of times any filter has been run for each filter applied.
- Adds new plotting method, scatter_filters, which shows which filtering step removed which time intervals of data in a plot of irradiance vs. power.
- New plotting method, timeseries_filters, which shows which fitlering step removed which time intervals of data in a plot of power vs. time.
- New plotting function, overlay_scatters, that overlays irradiance vs. power scatter plots of the data remaining after the last filtering step of the two CapData objects passed to the function.
- New get_filtering_table method that returns a DataFrame documenting the which time intervals are removed by which filter and which time intervals remain after all filtering.
- Adds the run_test function, which applies the passed list of CapData filtering methods to the CapData object passed.
- Adds the points_summary method, which prints the number of points remaining after all filtering, the length of the test period, the average points remaining after filtering per day, if enough points have been collected, if
more points are needed how many, and how many days left if the rate of points holds.

### Changed
- Updated filter_pvsyst method to handle inverter output variables that have underscores
or spaces like 'IL Pmin' and 'IL_Pmin'.
- load_das method no longer drops columns and rows that contain no data
- Format of hover tooltip in plots produced by plot method now includes comma separator for thousands.
- Changes captest to pvcaptest in documentation.
- get_reg_cols method default changed to get and rename the columns defined in the `regression_cols` attribute
rather than expecting regression variables/columns to be identified by the keys 'power', 'poa', 't_amb', and 'w_vel' in the `regression_cols` attribute.


[0.9.0]: https://github.com/pvcaptest/pvcaptest/compare/v0.8.0...v0.9.0
## [0.9.0] - 2020-08-16
### Changed
- Updated clear sky functions which rely on pandas `index.tz_localize` to use nonexistent argument rather than errors argument, which was deprecated in pandas v1.0.
- Made Pandas v1.0 or greater a requirement for pvcaptest.
- Change to test against python v3.7* and v3.8*
- Updated installation instructions.


[0.8.0]: https://github.com/pvcaptest/pvcaptest/compare/v0.7.0...v0.8.0
## [0.8.0] - 2020-04-13
### Added
- Added a filter_power method to the CapData class.
- Added a filter_days method to the CapData class.

### Changed
- Allow get_reg_cols to accept a single regression variable as a string. Previously required passing list with at least two entries.
- Fixed bug in filter_clearksy that applied filter to data rather than data_filtered attribute.
- Added option to plot method to use column names for hover labels instead of abbreviated column names.
- Improved formatting of the filtering summary output. See issue #12 for details.
- Cleaned up source code by correcting linter errors.

[0.7.0]: https://github.com/pvcaptest/pvcaptest/compare/v0.6.0...v0.7.0
## [0.7.0] - 2020-03-08
### Added
- New filter_shade method separate from the filter_pvsyst method.
- captest_results method warns when it automatically attempts to correct for W vs kW.

### Changed
- Filter_pvsyst method filters on IL Pmin, IL Pmax, IL Vmin, and IL Vmax and warns if any of the four are missing. Previously failed if any of the four were missing.
- cp_results returns a warning if the regression formulas of the passed CapData objects do not match instead of warning and continuing.
- Updates to make captest compatible with pvlib 0.7.0
- Editing of the complete capacity test example to use new names and improve explanations of features.

Names were changed to remove ambiguous abbreviations:
- flt - filter; API changes in many places
- cntg_eoy - wrap_year_end; API change
- cp_results - captest_results; API change
- res_summary - captest_results_check_pvalues; API change
- reg_fml - regression_formula; API change
- irrRC_balanced - irr_rc_balanced; API change
- df_beg - df_start
- ix_ser - ix_series
- mnth - month
- months_boy - months_year_start
- months_eoy - months_year_end
- loop_cnt - loop_count
- cprat - cap_ratio
- cprat_cpval - cap_ratio_check_pvalues
- trans - column_groups; API change
- set_translation - group_columns
- trans_report - column_type_report
- set_trans argument of load_data - group_columns
- review_trans - review_column_groups
- set_reg_trans - set_regression_cols
- reg_trans - regression_cols
- update_reg_trans argument of agg_sensors - update_regression_cols
- reg_cpt - fit_regression
- ols_model - regression_results

### Removed
- Removed the inv_trans_dict function. This was intended for use within the module and was unused.

[0.6.0]: https://github.com/pvcaptest/pvcaptest/compare/v0.5.3...v0.6.0
## [0.6.0] - 2019-09-15
### Added
- Setup Travis CI to test pull requests and test and deploy to pypi for tags on master.
- Setup project documentation hosted by Read the Docs using sphinx, nbshpinx, napolean, recommonmark, AutoStructify

### Changed
- Versioning changed from manual update in __version.py file to using versioneer to update version number from git tag.
- Updated this file to follow the Keep a Changelog formatting conventions.
- Moved repository to an organization github account from my personal github account.
- Examples moved from root/examples directory to docs/examples.
- Executed versions of the examples display on read the docs.
- All examples can be launched through binder in live notebooks.
- The environment file has been updated to work for binder and Read the Docs.

[0.5.3]: https://github.com/pvcaptest/pvcaptest/compare/v0.5.1...v0.5.3
## [0.5.3] - 2019-05-12
### Changed
- Update name and location of conda environment yml file, so there is a single file and it works with binder.
- Removed binder directory.
- Update readme to reflect changes to conda environment.yml
- Minor updates to example.
- Minor documentation string updates.

[0.5.1]: https://github.com/pvcaptest/pvcaptest/compare/v0.4.0...v0.5.1
## [0.5.1] - 2019-05-01
### Added
- Addition of clear sky modeling using pvlib library.  See new example notebook 'Clear Sky Examples'.
- Added a new method, `predict_capacities` for calculating reporting conditions and predicted outputs by month.
- New example notebook demonstrating use of `rep_cond` and `predict_capacities`.
- Add warning when filter removes all data.

### Changed
- Changed Holoviews dependency to >= v1.11.  DatLink added in v1.11 is required for scatter_hv method.
- Expanded docstring for the load_data method to more clearly explain how the method joins multiple files (by row).
- Update installation directions in README.
- Updated conda environment file (conda_env.yml) to match updated dependencies.
- **Moved all filtering and regression functionality from CapTest class into the CapData class and replace CapTest class with functions for results comparing CapData objects.**
- **Significant refactor of the rep\_cond function.  Removed any time filtering and prediction from rep\_cond.  Rep\_cond acts on filtered data in the df\_flt attribute.**
- `agg_sensors` method updated to be more explicit and flexible.
- Changed `filter_sensors` to filter based on percent difference between all combinations of pairs of sensors measuring the same environmental factor.  Corrected bug where standard deviation filter could not detect outliers with more than two, but still a small number of sensors.
- Adjusted bounds check of columns of data when importing so that translation dictionary names would not have 'valuesError' added to them.
- Made printout of bounds check results optional when loading data.
- Adjusted the type\_defs and sub\_type_defs, so that translation dictionary keys are more accurate for PVsyst data.
