pkg = import('pkgconfig')
g_ir_compiler = find_program('g-ir-compiler')

sample_src = [
    'Sample.vala',
    'SampleTest.vala'
]

sample_base_name = 'VunitTest' + '-' + meson.project_version()#'vunit-1.0.'
sample_gir = sample_base_name + '.gir'
sample_typelib = sample_base_name + '.typelib'

libsample = shared_library(
    'VunitTest',
    sample_src,
    dependencies : runner_dependencies,

    vala_header: 'VunitTest' + '.h',
    vala_vapi: 'VunitTest' + '-' + meson.project_version() + '.vapi',
    vala_gir: sample_gir,

    #version: meson.project_version(),
    install: false,
    install_dir: [false, false, false, false]
)

custom_target(sample_typelib,
    depends: libsample,
    command: [g_ir_compiler, '--shared-library', '@PLAINNAME@', '--output', '@OUTPUT@', '--includedir', vunit_build_dir, meson.current_build_dir() / sample_gir],
    input: libsample,
    output: sample_typelib,
    install: true,
    install_dir: get_option('libdir') / 'girepository-1.0')

#sample_pc = pkg.generate(
#    libsample,
#    name: sample_base_name,
#    requires: sample_deps,
#    description: 'A sample to try out VUnit against',
#    version: meson.project_version(),
#    url: 'https://github.com/Lindegaard-IT/VUnit'
#)
