(

  patch_it $SOURCE_CACHE/$SOURCE2 1 &&

  if ! in_depends $MODULE db; then
    sedit 's/arpd//' misc/Makefile
  fi &&

  chmod +x configure &&
  ./configure &&
  KERNEL_INCLUDE=/usr/include/ make SBINDIR=/usr/sbin &&
  prepare_install &&
  make SBINDIR=/usr/sbin install

) > $C_FIFO 2>&1
