mp_inc = include_directories(
  'core/include',
  'systems/include',
  'utility/include',
  )

cpp = meson.get_compiler('cpp')

mp_deps = []
mp_defines = []

if get_option('mp_units_api_freestanding')
  # no fmt/std::format, no exceptions: formatting headers self-guard via
  # bits/requires_hosted.h and #error out if included in this mode
  mp_defines = [
    '-DMP_UNITS_HOSTED=0',
    '-DMP_UNITS_API_FREESTANDING=1',
    ]
else
  mp_defines += ['-DMP_UNITS_HOSTED=1']

  # check for std::format
  std_format_supported = cpp.compiles(
    '''#include <format>
    #ifndef __cpp_lib_format
    #error "no std::format"
    #endif
    int main() { return 0; }''',
    name: 'std::format support',
    )

  use_std_format = get_option('mp_units_api_std_format') and std_format_supported

  mp_defines += [
    '-DMP_UNITS_API_STD_FORMAT=' + (use_std_format ? '1' : '0'),
    ]

  if not use_std_format
    mp_defines += ['-DMP_UNITS_USE_FMTLIB']
    fmt_sub = subproject('fmt', default_options: ['fmt_test=false', 'fmt_header_only=true'])
    fmt_dep = fmt_sub.get_variable('fmt_header_only_dep')
    mp_deps += [fmt_dep]
  endif
endif
