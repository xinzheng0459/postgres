intarray_sources = files(
  '_int_bool.c',
  '_int_gin.c',
  '_int_gist.c',
  '_int_op.c',
  '_int_selfuncs.c',
  '_int_tool.c',
  '_intbig_gist.c',
)

intarray = shared_module('_int',
  intarray_sources,
  kwargs: contrib_mod_args,
)
contrib_targets += intarray

install_data(
  'intarray.control',
  'intarray--1.0--1.1.sql',
  'intarray--1.1--1.2.sql',
  'intarray--1.2.sql',
  'intarray--1.2--1.3.sql',
  'intarray--1.3--1.4.sql',
  'intarray--1.4--1.5.sql',
  kwargs: contrib_data_args,
)

tests += {
  'name': 'intarray',
  'sd': meson.current_source_dir(),
  'bd': meson.current_build_dir(),
  'regress': {
    'sql': [
      '_int',
    ],
  },
}
