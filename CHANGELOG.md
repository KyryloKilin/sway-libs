# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [Unreleased] - yyyy-mm-dd

Description of the upcoming release here.

### Added

- [#259](https://github.com/FuelLabs/sway-libs/pull/259) Adds a new upgradability library, including associated tests and documentation.
- [#265](https://github.com/FuelLabs/sway-libs/pull/265) Adds the `SetMetadataEvent` and emits `SetMetadataEvent` when the `_set_metadata()` function is called.
- [#270](https://github.com/FuelLabs/sway-libs/pull/270) Adds `OrdEq` functionality to Signed Integers.
- [#272](https://github.com/FuelLabs/sway-libs/pull/272) Adds the `TryFrom` implementation from signed integers to unsigned integers.

### Changed

- [#265](https://github.com/FuelLabs/sway-libs/pull/265) Enables the metadata events now that the Rust SDK supports wrapped heap types.
- [#269](https://github.com/FuelLabs/sway-libs/pull/269) Hashes the string "admin" and with the bits of an Identity when creating a storage slot to storage an admin in the Admin Library.
- [#278](https://github.com/FuelLabs/sway-libs/pull/278) Deprecates the Fixed Point number library.

### Fixed

- [#258](https://github.com/FuelLabs/sway-libs/pull/258) Fixes incorrect instructions on how to run tests in README and docs hub.
- [#262](https://github.com/FuelLabs/sway-libs/pull/262) Fixes incorrect ordering comparison for IFP64, IFP128 and IFP256.
- [#263](https://github.com/FuelLabs/sway-libs/pull/263) Fixes `I256`'s returned bits.
- [#263](https://github.com/FuelLabs/sway-libs/pull/263) Fixes `I128` and `I256`'s zero or "indent" value.
- [#268](https://github.com/FuelLabs/sway-libs/pull/268) Fixes subtraction involving negative numbers for `I8`, `I16`, `I32`, `I64`, `I128`, and `I256`.
- [#272](https://github.com/FuelLabs/sway-libs/pull/272) Fixes `From` implementations for Signed Integers with `TryFrom`.
- [#273](https://github.com/FuelLabs/sway-libs/pull/273) Fixes negative from implementations for Signed Integers.

#### Breaking

- [#263](https://github.com/FuelLabs/sway-libs/pull/263) Removes the `TwosComplement` trait in favor of `WrappingNeg`.

The following demonstrates the breaking change. While this example code uses the `I8` type, the same logic may be applied to the `I16`, `I32`, `I64`, `I128`, and `I256` types.

Before:

```sway
let my_i8 = i8::zero();
let twos_complement = my_i8.twos_complement();
```

After:

```sway
let my_i8 = i8::zero();
let wrapping_neg = my_i8.wrapping_neg();
```

- [#272](https://github.com/FuelLabs/sway-libs/pull/272) The `From` implementation for all signed integers to their respective unsigned integer has been removed. The `TryFrom` implementation has been added in its place.

Before:

```sway
let my_i8: I8 = I8::from(1u8);
```

After:

```sway
let my_i8: I8 = I8::try_from(1u8).unwrap();
```

- [#273](https://github.com/FuelLabs/sway-libs/pull/273) The `neg_from` implementation for all signed integers has been removed. The `neg_try_from()` implementation has been added in its place.

The following demonstrates the breaking change. While this example code uses the `I8` type, the same logic may be applied to the `I16`, `I32`, `I64`, `I128`, and `I256` types.

Before:

```sway
let my_negative_i8: I8 = I8::neg_from(1u8);
```

After:

```sway
let my_negative_i8: I8 = I8::neg_try_from(1u8).unwrap();
```

- [#278](https://github.com/FuelLabs/sway-libs/pull/278) Deprecates the Fixed Point number library. The Fixed Point number library is no longer available.