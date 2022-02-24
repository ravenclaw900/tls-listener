# Changelog

## 0.4.0 - 2022-02-22

NOTE: This release contains several breaking changes.

### Added

- Support for [`native-tls`](https://github.com/sfackler/rust-native-tls).

### Changed

- The TLS backend is now configurable. Both rustls and native-tls are supported. Other backends can also be used by implementing the `AsyncTls` trait.
  - You must now supply either the `rustls` or `native-tls` features to get support for a tls backend.
  - Unfortunately, the machinery for this required adding an additional type parameter to `TlsListener`.
- The `TlsListener` stream now returns a `tls_listener::Error` instead of `std::io::Error` type.
- Signatures of `TcpListener::new()` and `builder()` have changed to now take an argument of the TLS type rather than a `rustls::ServerConfig`,
  to update existing calls, replace `builder(config)` with `builder(Arc::new(config).into())`.

### Fixed

- Crate will now compile when linked against a target that doesn't explicitly enable the `tokio/time` and `hyper/tcp`
  features.