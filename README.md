Rust-chrono
===========

[![Rust-chrono on Travis CI][travis-image]][travis]

[travis-image]: https://travis-ci.org/lifthrasiir/rust-chrono.png
[travis]: https://travis-ci.org/lifthrasiir/rust-chrono

Date and time handling for Rust.

```rust
// find out if the doomsday rule is correct!
use chrono::{MIN_YEAR, MAX_YEAR, Weekday, DateZ};
use std::iter::range_inclusive;

for y in range_inclusive(MIN_YEAR, MAX_YEAR) {
    // even months
    let d4   = DateZ::from_ymd(y,  4,  4);
    let d6   = DateZ::from_ymd(y,  6,  6);
    let d8   = DateZ::from_ymd(y,  8,  8);
    let d10  = DateZ::from_ymd(y, 10, 10);
    let d12  = DateZ::from_ymd(y, 12, 12);

    // nine to five, seven-eleven
    let d59  = DateZ::from_ymd(y,  5,  9);
    let d95  = DateZ::from_ymd(y,  9,  5);
    let d711 = DateZ::from_ymd(y,  7, 11);
    let d117 = DateZ::from_ymd(y, 11,  7);

    // "March 0"
    let d30  = DateZ::from_ymd(y,  3,  1).pred();

    let weekday = d30.weekday();
    let other_dates = [d4, d6, d8, d10, d12, d59, d95, d711, d117];
    assert!(other_dates.iter().all(|d| d.weekday() == weekday));
}
```

Design Goals
------------

* 1-to-1 correspondence with ISO 8601.
* Timezone-aware by default.
* Space efficient.
* Moderate lookup table size, should not exceed a few KBs.
* Avoid divisions as much as possible.

References
----------

* https://github.com/mozilla/rust/wiki/Lib-datetime
* https://github.com/luisbg/rust-datetime/wiki/Use-Cases

