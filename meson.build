project('mp-units',
  'cpp',
  version: '2.5.0',
  license: 'MIT',
  meson_version: '>=1.1.0',
  default_options: [
    'cpp_std=c++23',
    'warning_level=3',
    ],
  )

subdir('src')
mp_dep = declare_dependency(
  include_directories: mp_inc,
  compile_args: mp_defines,
  dependencies: mp_deps,
  )
