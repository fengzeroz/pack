# pack
ubuntu package make

import mkdeb
import os

rules = []
rules.append(mkdeb.FileMap(
    "sss.so", "/usr/lib/yyy/"))
rules.append(mkdeb.FileMap(
"exe", "/opt/yyy/sbin/", "x"))

#control file
rules.append(mkdeb.FileMap("./config/ubuntu/DEBIAN/conffiles_cpe",
                           "/DEBIAN/", "r", "conffiles"))
rules.append(mkdeb.FileMap("./config/ubuntu/DEBIAN/postinst",
                           "/DEBIAN/", "r", "postinst"))
rules.append(mkdeb.FileMap("./config/ubuntu/DEBIAN/preinst",
                           "/DEBIAN/", "r", "preinst"))
rules.append(mkdeb.FileMap("./config/ubuntu/DEBIAN/prerm",
                           "/DEBIAN/", "r", "prerm"))

mkdeb.create_deb_file(rules)
mkdeb.create_control(
    'aiwan-orion-client', sys.argv[1], "x86_64", "collectd plugin", "")
#openwrt ipk
mkdeb.create_ipkg('aiwan-orion-client',
                  sys.argv[1], 'x86_64')

#ubuntu deb
cmd = 'dpkg-deb -b tmp/ ' + pktname + '_' + sys.argv[1] + "_amd64.deb"
os.system(cmd)