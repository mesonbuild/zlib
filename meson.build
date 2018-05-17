project('zlib', 'c', version : '1.2.11', license : 'zlib')

cc = meson.get_compiler('c')
if cc.get_id() == 'msvc'
  add_project_arguments(
    '-D_CRT_SECURE_NO_DEPREACATE', '-D_CRT_NONSTDC_NO_DEPRECATE',
    language : ['c']
  )
endif

src = files([
  'adler32.c',
  'crc32.c',
  'deflate.c',
  'infback.c',
  'inffast.c',
  'inflate.c',
  'inftrees.c',
  'trees.c',
  'zutil.c',
  'compress.c',
  'uncompr.c',
  'gzclose.c',
  'gzlib.c',
  'gzread.c',
  'gzwrite.c'])

if host_machine.system() == 'windows'
  win = import('windows')
  win_args = []
  if cc.get_id() != 'msvc'
    win_args += '-DGCC_WINDRES'
  endif
  src += win.compile_resources('win32/zlib1.rc', args : win_args)
endif

if get_option('asm')
  if host_machine.cpu_family().startswith('x86')
    if cc.get_id() == 'msvc'
      if host_machine.cpu_family() == 'x86'
        src += files(
          'contrib/masmx86/inffas32.asm',
          'contrib/masmx86/match686.asm',
        )
      else
        src += files(
          'contrib/masmx86/inffasx64.asm',
          'contrib/masmx86/gvmat64.asm',
        )
      endif
      add_project_arguments('-DASMV', '-DASMINF', language : ['c'])
    else
      if host_machine.cpu_family() == 'x86'
        src += files('contrib/asm686/match.S')
      else
        src += files('contrib/amd64/amd64-match.S')
      endif
      add_project_arguments('-DASMV', '-DNO_UNDERLINE', language : ['c'])
    endif
  endif
endif

zlib = library(
  'z',
  src,
  vs_module_defs : 'win32/zlib.def',
)

incdir = include_directories('.')

zlib_dep = declare_dependency(
  link_with : zlib,
  include_directories : incdir)
