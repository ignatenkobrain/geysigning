glib = dependency('glib-2.0')
gpgme = find_library('gpgme')
gtk = dependency('gtk+-3.0')

add_global_arguments('-DG_LOG_DOMAIN="GnomeKeySign"', language : 'c')

libkeysign = static_library('keysign',
                            'gks-gpg.c', 'gks-gpg.h',
                            dependencies : [glib, gpgme],
                            install : false)

executable('gnome-keysign',
           'gks-main.c',
           dependencies : [glib, gpgme, gtk],
           link_with : libkeysign)
