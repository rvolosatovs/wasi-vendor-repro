`wasi` crate from https://github.com/bytecodealliance/preview2-prototyping/tree/b871bec0ed3b21ec8fcd6f1bb7e48d8c186016f9/wasi is incompatible with `cargo vendor`

Try (from root of this repository):

```shell
$ cargo vendor
$ cargo build
```

Fails with:
```
   Compiling wasi v0.12.0+wasi-snapshot-preview2 (https://github.com/bytecodealliance/preview2-prototyping#083879cb)
error: failed to read file "/home/rvolosatovs/src/github.com/rvolosatovs/repro/vendor/wasi/../wit"
       
       Caused by:
           No such file or directory (os error 2)
       
       Stack backtrace:
          0: <E as anyhow::context::ext::StdError>::ext_context
          1: anyhow::context::<impl anyhow::Context<T,E> for core::result::Result<T,E>>::with_context
          2: wit_parser::UnresolvedPackage::parse_file
          3: wit_bindgen_rust_macro::parse_source::{{closure}}
          4: wit_bindgen_rust_macro::parse_source
          5: <wit_bindgen_rust_macro::Config as syn::parse::Parse>::parse
          6: <T as syn::parse_macro_input::ParseMacroInput>::parse
          7: core::ops::function::FnOnce::call_once
          8: <F as syn::parse::Parser>::parse2
          9: syn::parse::Parser::parse
         10: syn::parse_macro_input::parse
         11: wit_bindgen_rust_macro::generate
         12: core::ops::function::Fn::call
         13: proc_macro::bridge::client::Client<proc_macro::TokenStream,proc_macro::TokenStream>::expand1::{{closure}}::{{closure}}
         14: proc_macro::bridge::client::run_client::{{closure}}::{{closure}}::{{closure}}
         15: proc_macro::bridge::scoped_cell::ScopedCell<T>::set::{{closure}}
         16: proc_macro::bridge::scoped_cell::ScopedCell<T>::replace
         17: proc_macro::bridge::scoped_cell::ScopedCell<T>::set
         18: proc_macro::bridge::client::run_client::{{closure}}::{{closure}}
         19: std::thread::local::LocalKey<T>::try_with
         20: std::thread::local::LocalKey<T>::with
         21: proc_macro::bridge::client::run_client::{{closure}}
         22: <core::panic::unwind_safe::AssertUnwindSafe<F> as core::ops::function::FnOnce<()>>::call_once
         23: std::panicking::try::do_call
         24: __rust_try
         25: std::panicking::try
         26: std::panic::catch_unwind
         27: proc_macro::bridge::client::run_client
         28: proc_macro::bridge::client::Client<proc_macro::TokenStream,proc_macro::TokenStream>::expand1::{{closure}}
         29: proc_macro::bridge::selfless_reify::reify_to_extern_c_fn_hrt_bridge::wrapper
         30: <proc_macro::bridge::server::MaybeCrossThread<rustc_expand::proc_macro::CrossbeamMessagePipe<proc_macro::bridge::buffer::Buffer>> as proc_macro::bridge::server::ExecutionStrategy>::run_bridge_and_client::<proc_macro::bridge::server::Dispatcher<proc_macro::bridge::server::MarkedTypes<rustc_expand::proc_macro_server::Rustc>>>
         31: proc_macro::bridge::server::run_server::<rustc_expand::proc_macro_server::Rustc, proc_macro::bridge::Marked<rustc_ast::tokenstream::TokenStream, proc_macro::bridge::client::TokenStream>, core::option::Option<proc_macro::bridge::Marked<rustc_ast::tokenstream::TokenStream, proc_macro::bridge::client::TokenStream>>, proc_macro::bridge::server::MaybeCrossThread<rustc_expand::proc_macro::CrossbeamMessagePipe<proc_macro::bridge::buffer::Buffer>>>
         32: <proc_macro::bridge::client::Client<proc_macro::TokenStream, proc_macro::TokenStream>>::run::<rustc_expand::proc_macro_server::Rustc, proc_macro::bridge::server::MaybeCrossThread<rustc_expand::proc_macro::CrossbeamMessagePipe<proc_macro::bridge::buffer::Buffer>>>
         33: <rustc_expand::proc_macro::BangProcMacro as rustc_expand::base::BangProcMacro>::expand
         34: <rustc_expand::expand::MacroExpander>::fully_expand_fragment
         35: <rustc_expand::expand::MacroExpander>::expand_crate
         36: <rustc_session::session::Session>::time::<rustc_ast::ast::Crate, rustc_interface::passes::configure_and_expand::{closure#1}>
         37: rustc_interface::passes::resolver_for_lowering
         38: rustc_query_system::query::plumbing::try_execute_query::<rustc_query_impl::queries::resolver_for_lowering, rustc_query_impl::plumbing::QueryCtxt>
         39: <rustc_query_impl::Queries as rustc_middle::ty::query::QueryEngine>::resolver_for_lowering
         40: <rustc_middle::ty::context::GlobalCtxt>::enter::<rustc_driver_impl::run_compiler::{closure#1}::{closure#2}::{closure#2}, &rustc_data_structures::steal::Steal<(rustc_middle::ty::ResolverAstLowering, alloc::rc::Rc<rustc_ast::ast::Crate>)>>
         41: <rustc_interface::interface::Compiler>::enter::<rustc_driver_impl::run_compiler::{closure#1}::{closure#2}, core::result::Result<core::option::Option<rustc_interface::queries::Linker>, rustc_span::ErrorGuaranteed>>
         42: rustc_span::with_source_map::<core::result::Result<(), rustc_span::ErrorGuaranteed>, rustc_interface::interface::run_compiler<core::result::Result<(), rustc_span::ErrorGuaranteed>, rustc_driver_impl::run_compiler::{closure#1}>::{closure#0}::{closure#0}>
         43: std::sys_common::backtrace::__rust_begin_short_backtrace::<rustc_interface::util::run_in_thread_pool_with_globals<rustc_interface::interface::run_compiler<core::result::Result<(), rustc_span::ErrorGuaranteed>, rustc_driver_impl::run_compiler::{closure#1}>::{closure#0}, core::result::Result<(), rustc_span::ErrorGuaranteed>>::{closure#0}::{closure#0}, core::result::Result<(), rustc_span::ErrorGuaranteed>>
         44: <<std::thread::Builder>::spawn_unchecked_<rustc_interface::util::run_in_thread_pool_with_globals<rustc_interface::interface::run_compiler<core::result::Result<(), rustc_span::ErrorGuaranteed>, rustc_driver_impl::run_compiler::{closure#1}>::{closure#0}, core::result::Result<(), rustc_span::ErrorGuaranteed>>::{closure#0}::{closure#0}, core::result::Result<(), rustc_span::ErrorGuaranteed>>::{closure#1} as core::ops::function::FnOnce<()>>::call_once::{shim:vtable#0}
         45: <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once
                    at /rustc/2036fdd24f77d607dcfaa24c48fbe85d3f785823/library/alloc/src/boxed.rs:1988:9
         46: <alloc::boxed::Box<F,A> as core::ops::function::FnOnce<Args>>::call_once
                    at /rustc/2036fdd24f77d607dcfaa24c48fbe85d3f785823/library/alloc/src/boxed.rs:1988:9
         47: std::sys::unix::thread::Thread::new::thread_start
                    at /rustc/2036fdd24f77d607dcfaa24c48fbe85d3f785823/library/std/src/sys/unix/thread.rs:108:17
         48: start_thread
         49: clone3
  --> /home/rvolosatovs/src/github.com/rvolosatovs/repro/vendor/wasi/src/lib.rs:6:9
   |
6  | /         wit_bindgen::generate!({
7  | |             path: "../wit",
8  | |             world: "reactor",
9  | |             std_feature,
10 | |         });
   | |__________^
   |
   = note: this error originates in the macro `wit_bindgen::generate` (in Nightly builds, run with -Z macro-backtrace for more info)
```
