pgbench_sources = files(
  'pgbench.c',
)

exprscan = custom_target('exprscan',
  input: 'exprscan.l',
  output: 'exprscan.c',
  command: flex_cmd,
)
generated_sources += exprscan
pgbench_sources += exprscan

exprparse = custom_target('exprparse',
  input: 'exprparse.y',
  kwargs: bison_kw,
)
generated_sources += exprparse.to_list()
pgbench_sources += exprparse

pgbench = executable('pgbench',
  pgbench_sources,
  dependencies: [frontend_code, libpq, thread_dep],
  include_directories: include_directories('.'),
  kwargs: default_bin_args,
)
bin_targets += pgbench

tests += {
  'name': 'pgbench',
  'sd': meson.current_source_dir(),
  'bd': meson.current_build_dir(),
  'tap': {
    'tests': [
      't/001_pgbench_with_server.pl',
      't/002_pgbench_no_server.pl',
    ],
  },
}
