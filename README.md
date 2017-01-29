## Based on
https://www.dropbox.com/sh/t52c02rm20y8x9p/khFGAJu3gc

## HOWTO

./WNDR3700-trunk-r50082-20170122-1044-newBuildroot.sh

cd trunk

./hnscripts/updateNmake.sh

scp XXX-sysupgrade.bin root@192.168.1.1:/tmp

ssh root@192.168.1.1

cd /tmp

sysupgrade -v XXX-sysupgrade.bin

curl http://192.168.1.1:8080/
