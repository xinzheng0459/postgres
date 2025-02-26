psql_sources = files(
  'command.c',
  'common.c',
  'copy.c',
  'crosstabview.c',
  'describe.c',
  'help.c',
  'input.c',
  'large_obj.c',
  'mainloop.c',
  'prompt.c',
  'startup.c',
  'stringutils.c',
  'tab-complete.c',
  'variables.c',
)

psqlscanslash = custom_target('psqlscanslash',
  input: 'psqlscanslash.l',
  output: 'psqlscanslash.c',
  command: [flex_cmd, '--no-backup', '--fix-warnings', '--', '-Cfe', '-p', '-p'])
generated_sources += psqlscanslash
psql_sources += psqlscanslash

sql_help = custom_target('psql_help',
  output: ['sql_help.c', 'sql_help.h'],
  depfile: 'sql_help.dep',
  command: [
    perl, files('create_help.pl'),
    '--docdir', '@SOURCE_ROOT@/doc/src/sgml/ref',
    '--depfile', '@DEPFILE@',
    '--outdir', '@OUTDIR@',
    '--basename', 'sql_help',
  ],
)
generated_sources += sql_help.to_list()
psql_sources += sql_help

psql = executable('psql',
  psql_sources,
  include_directories: include_directories('.'),
  dependencies: [frontend_code, libpq, readline],
  kwargs: default_bin_args,
)
bin_targets += psql

install_data('psqlrc.sample',
  install_dir: dir_data,
)

tests += {
  'name': 'psql',
  'sd': meson.current_source_dir(),
  'bd': meson.current_build_dir(),
  'tap': {
    'env': {'with_readline': readline.found() ? 'yes' : 'no'},
    'tests': [
      't/001_basic.pl',
      't/010_tab_completion.pl',
      't/020_cancel.pl',
    ],
  },
}

subdir('po', if_found: libintl)
