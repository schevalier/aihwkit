
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog], and this project adheres to
[Semantic Versioning]:

* `Added` for new features.
* `Changed` for changes in existing functionality.
* `Deprecated` for soon-to-be removed features.
* `Removed` for now removed features.
* `Fixed` for any bug fixes.
* `Security` in case of vulnerabilities.


## [UNRELEASED]

### Added

* The `rpu_config` is now pretty-printed in a readable manner (excluding the
  default settings and other readability tweak). (\#60)
* Added a new `ReferenceUnitCell` which has two devices, where one is fixed and
  the other updated and the effective weight is computed a difference between
  the two. (\#61)
* `VectorUnitCell` accepts now arbitrary weighting schemes that can be
  user-defined by using a new `gamma_vec` property that specifies how to combine
  the unit cell devices to form the effective weight. (\#61)

### Changed

* The unit cell items in `aihwkit.simulator.configs` have been renamed, removing
  their `Device` suffix, for having a more consistent naming scheme. (\#57)
* The `Exceptions` raised by the library have been revised, making use in some
  cases of the ones introduced in a new `aihwkit.exceptions` module. (\#49)
* The `pybind11` version required has been bumped to 2.6.0, which can be
  installed from `pip` and makes system-wide installation no longer required.
  Please update your `pybind11` accordingly for compiling the library. (\#44)
* Some `VectorUnitCell` properties have been renamed and extended with an update
  policy specifying how to select the hidden devices. (\#61)

### Removed

* The `BackwardIOParameters` specialization has been removed, as bound
  management is now automatically ignored for the backward pass. Please use the
  more general `IOParameters` instead. (\#45)

### Fixed

* Serialization of `Modules` that contain children analog layers is now
  possible, both when using containers such as `Sequential` and when using
  analog layers as custom Module attributes. (\#74)
* The build system has been improved, with experimental Windows support and
  supporting using CUDA 11 correctly. (\#58, \#67, \#68)

## [0.2.0] - 2020/10/20

### Added

* Added more types of resistive devices: `IdealResistiveDevice`, `LinearStep`,
  `SoftBounds`, `ExpStep`, `VectorUnitCell`, `TransferCompoundDevice`,
  `DifferenceUnitCell`. (\#14)
* Added a new `InferenceTile` that supports basic hardware-aware training
  and inference using a statistical noise model that was fitted by real PCM
  devices. (\#25)
* Added a new `AnalogSequential` layer that can be used in place of `Sequential`
  for easier operation on children analog layers. (\#34)

### Changed

* Specifying the tile configuration (resistive device and the rest of the
  properties) is now based on a new `RPUConfig` family of classes, that is
  passed as a `rpu_config` argument instead of `resistive_device` to `Tiles`
  and `Layers`. Please check the `aihwkit.simulator.config` module for more
  details. (\#23)
* The different analog tiles are now organized into a `aihwkit.simulator.tiles`
  package. The internal `IndexedTiles` have been removed, and the rest of
  previous top-level imports have been kept. (\#29)

### Fixed

* Improved package compatibility when using non-UTF8 encodings (version file,
  package description). (\#13)
* The build system can now detect and use `openblas` directly when using the
  conda-installable version. (\#22)
* When using analog layers as children of another module, the tiles are now
  correctly moved to CUDA if using `AnalogSequential` (or by the optimizer if
  using regular torch container modules). (\#34)

## [0.1.0] - 2020/09/17

### Added

* Initial public release.
* Added `rpucuda` C++ simulator, exposed through a `pybind` interface.
* Added a PyTorch `AnalogLinear` neural network model.
* Added a PyTorch `AnalogConv2d` neural network model.


[UNRELEASED]: https://github.com/IBM/aihwkit/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/IBM/aihwkit/compare/v0.1.0..v0.2.0
[0.1.0]: https://github.com/IBM/aihwkit/releases/tag/v0.1.0

[Keep a Changelog]: https://keepachangelog.com/en/1.0.0/
[Semantic Versioning]: https://semver.org/spec/v2.0.0.html
