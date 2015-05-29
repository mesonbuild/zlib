project('zlib', 'c')

src = ['adler32.c', 'crc32.c', 'deflate.c', 'infback.c', 'inffast.c', 'inflate.c',
'inftrees.c', 'trees.c', 'zutil.c',
'compress.c', 'uncompr.c', 'gzclose.c', 'gzlib.c', 'gzread.c', 'gzwrite.c']

if get_option('shared_lib')
  zlib = shared_library('z', src)
else
  zlib = static_library('z', src)
endif

incdir = include_directories('.')
