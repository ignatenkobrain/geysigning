glib = dependency('glib-2.0')
gpgme = find_library('gpgme')
gtk = dependency('gtk+-3.0')

gres = find_program('glib-compile-resources')

add_global_arguments('-DG_LOG_DOMAIN="GnomeKeySign"', language : 'c')

libkeysign = static_library('keysign',
                            'gks-gpg.c', 'gks-gpg.h',
                            dependencies : [glib, gpgme],
                            install : false)

resources_c = custom_target('gks-resources.c',
  output : 'gks-resources.c',
  input : 'gnome-keysign.gresource.xml',
  command : [gres, '--target', '@OUTPUT@', '--c-name=gks', '--generate-source',
             '--sourcedir=../data', '@INPUT@'],
)

resources_h = custom_target('gks-resources.h',
  output : 'gks-resources.h',
  input : 'gnome-keysign.gresource.xml',
  command : [gres, '--target', '@OUTPUT@', '--c-name=gks', '--generate-header',
             '--sourcedir=../data', '@INPUT@'],
)

executable('gnome-keysign',
           'gks-main.c', resources_c, resources_h,
           dependencies : [glib, gpgme, gtk],
           link_with : libkeysign)
