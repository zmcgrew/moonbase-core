(

  CFLAGS+=" -fPIE "
  LDFLAGS+=" -pie "

  if module_installed systemd; then
    OPTS+=" --with-udev_prefix=/usr \
            --with-systemdsystemunitdir=$(pkg-config systemd --variable=systemdsystemunitdir)"
  else
    OPTS+=" --with-udev_prefix=/"
  fi &&


  ./configure  --sbindir=/sbin                \
               --libdir=/lib                  \
               --enable-cmdlib                \
               --enable-pkgconfig             \
               --with-optimisation="$CFLAGS"  \
               --enable-fsadm                 \
               --enable-dmeventd              \
               --enable-applib                \
               --enable-udev_sync             \
               --enable-udev_rules            \
               $OPTS                         &&

  default_make &&
  make install_system_dirs

) > $C_FIFO 2>&1
