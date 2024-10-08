project('CTMF', 'cpp',
  default_options: ['buildtype=release', 'b_ndebug=if-release', 'cpp_std=c++17'],
  meson_version: '>=0.48.0',
  version: '5'
)

sources = [
  'CTMF/CTMF.cpp',
  'CTMF/CTMF.h'
]
sources += [
    'CTMF/CTMF_SSE2.cpp',
    'CTMF/VCL2/instrset.h',
    'CTMF/VCL2/instrset_detect.cpp',
    'CTMF/VCL2/vector_convert.h',
    'CTMF/VCL2/vectorclass.h',
    'CTMF/VCL2/vectorf128.h',
    'CTMF/VCL2/vectorf256.h',
    'CTMF/VCL2/vectorf256e.h',
    'CTMF/VCL2/vectorf512.h',
    'CTMF/VCL2/vectorf512e.h',
    'CTMF/VCL2/vectori128.h',
    'CTMF/VCL2/vectori256.h',
    'CTMF/VCL2/vectori256e.h',
    'CTMF/VCL2/vectori512.h',
    'CTMF/VCL2/vectori512e.h',
    'CTMF/VCL2/vectori512s.h',
    'CTMF/VCL2/vectori512se.h',
    'CTMF/VCL2/vectormath_common.h',
    'CTMF/VCL2/vectormath_exp.h',
    'CTMF/VCL2/vectormath_hyp.h',
    'CTMF/VCL2/vectormath_lib.h',
    'CTMF/VCL2/vectormath_trig.h'
  ]

vapoursynth_dep = dependency('vapoursynth').partial_dependency(compile_args: true, includes: true)

libs = []

if host_machine.cpu_family().startswith('x86')
  add_project_arguments('-fno-math-errno', '-fno-trapping-math', '-DCTMF_X86', '-mfpmath=sse', '-msse2', language: 'cpp')

  sources += [
    'CTMF/CTMF_SSE2.cpp',
    'CTMF/VCL2/instrset.h',
    'CTMF/VCL2/instrset_detect.cpp',
    'CTMF/VCL2/vector_convert.h',
    'CTMF/VCL2/vectorclass.h',
    'CTMF/VCL2/vectorf128.h',
    'CTMF/VCL2/vectorf256.h',
    'CTMF/VCL2/vectorf256e.h',
    'CTMF/VCL2/vectorf512.h',
    'CTMF/VCL2/vectorf512e.h',
    'CTMF/VCL2/vectori128.h',
    'CTMF/VCL2/vectori256.h',
    'CTMF/VCL2/vectori256e.h',
    'CTMF/VCL2/vectori512.h',
    'CTMF/VCL2/vectori512e.h',
    'CTMF/VCL2/vectori512s.h',
    'CTMF/VCL2/vectori512se.h',
    'CTMF/VCL2/vectormath_common.h',
    'CTMF/VCL2/vectormath_exp.h',
    'CTMF/VCL2/vectormath_hyp.h',
    'CTMF/VCL2/vectormath_lib.h',
    'CTMF/VCL2/vectormath_trig.h'
  ]

  libs += static_library('avx2', 'CTMF/CTMF_AVX2.cpp',
    dependencies: vapoursynth_dep,
    cpp_args: ['-mavx2', '-mfma'],
    gnu_symbol_visibility: 'hidden'
  )

  libs += static_library('avx512', 'CTMF/CTMF_AVX512.cpp',
    dependencies: vapoursynth_dep,
    cpp_args: ['-mavx512f', '-mavx512vl', '-mavx512bw', '-mavx512dq', '-mfma'],
    gnu_symbol_visibility: 'hidden'
  )
endif

shared_module('ctmf', sources,
  dependencies: vapoursynth_dep,
  link_with: libs,
  install: true,
  install_dir: join_paths(vapoursynth_dep.get_pkgconfig_variable('libdir'), 'vapoursynth'),
  gnu_symbol_visibility: 'hidden'
)
