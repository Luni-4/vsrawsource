project('vsrawsource', 'c',
        version: '1',
        default_options: ['c_std=gnu99', 'buildtype=release'],
        meson_version: '>=0.46')


warnings = [
  '-Wall',
  '-Wextra',
  '-Wno-unused-parameter',
  '-Wshadow'
]

cflags = [
  warnings,
  '-ffast-math',
  '-fomit-frame-pointer',
  '-fexcess-precision=fast'
]

ldflags = [
]

host_cpu_family = host_machine.cpu_family()

if host_cpu_family.startswith('x86')
  cflags += ['-mfpmath=sse', '-msse2']
endif

host_system = host_machine.system()

if host_system == 'windows' or host_system == 'cygwin'
  if host_cpu_family == 'x86'
    ldflags += '-Wl,--kill-at'
  endif
endif

cc = meson.get_compiler('c')


sources = [
  'src/rawsource.c'
]

deps = [
  dependency('vapoursynth').partial_dependency(
      includes: true,
      compile_args: true),
]

shared_module('vsrawsource',
              sources,
              dependencies: deps,
              link_args: ldflags,
              c_args: cflags,
              install: true)
