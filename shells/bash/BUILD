(

  bad_flags -malign-double  &&

  patch_it $SOURCE2  0  &&
  patch_it $SOURCE3  0  &&
  patch_it $SOURCE4  0  &&
  patch_it $SOURCE5  0  &&
  patch_it $SOURCE6  0  &&
  patch_it $SOURCE7  0  &&
  patch_it $SOURCE8  0  &&
  patch_it $SOURCE9  0  &&
  patch_it $SOURCE10 0  &&
  patch_it $SOURCE11 0  &&
  patch_it $SOURCE12 0  &&
  patch_it $SOURCE13 0  &&
  patch_it $SOURCE14 0  &&
  patch_it $SOURCE15 0  &&
  patch_it $SOURCE16 0  &&
  patch_it $SOURCE17 0  &&
  patch_it $SOURCE18 0  &&
  patch_it $SOURCE19 0  &&
  patch_it $SOURCE20 0  &&
  patch_it $SOURCE21 0  &&
  patch_it $SOURCE22 0  &&
  patch_it $SOURCE23 0  &&
  patch_it $SOURCE24 0  &&
  patch_it $SOURCE25 0  &&
  patch_it $SOURCE26 0  &&
  patch_it $SOURCE27 0  &&
  patch_it $SOURCE28 0  &&
  patch_it $SOURCE29 0  &&
  patch_it $SOURCE30 0  &&
  patch_it $SOURCE31 0  &&
  patch_it $SOURCE32 0  &&
  patch_it $SOURCE33 0  &&
  patch_it $SOURCE34 0  &&
  patch_it $SOURCE35 0  &&
  patch_it $SOURCE36 0  &&
  patch_it $SOURCE37 0  &&
  patch_it $SOURCE38 0  &&

  OPTS+=" --bindir=/bin                 \
          --enable-readline             \
          --without-installed-readline  \
          --with-curses                 \
          --without-bash-malloc         \
          --disable-profiling"         &&

  default_build  &&
  ln -sf bash /bin/sh  &&
  ln -f /bin/bash /bin/rbash  &&

  rm -f /usr/share/man/man1/bash.1  &&
  rm -f /usr/share/man/man1/bashbug.1  &&

  for MANPAGE in doc/*.1 ; do
    gzip -9 $MANPAGE  &&
    install -m0644 $MANPAGE.gz /usr/share/man/man1
  done  &&
  install -m0644 doc/bashref.info /usr/share/info  &&

  mkdir -p /etc/skel  &&

  if [ -L /etc/skel/.bashrc ] ; then
    rm /etc/skel/.bashrc
  fi  &&

  if [ -f /etc/profile.d ] ; then
    rm /etc/profile.d
  fi  &&

  if [ ! -d /etc/profile.d ]; then
    mkdir -p /etc/profile.d
    message "${MESSAGE_COLOR}"
    message "Since 20020808 bash comes with a new way to manage profiles and"
    message "package settings for the shell. This will allow lunar to auto-"
    message "matically install the proper shell variables for each module."
    message ""
    message "With this set of profile files come 2 new systemwide files: "
    message "/etc/profile and /etc/bashrc, made as they should be for "
    message "proper functionality of the system. If you wish, they will be"
    message "backed up and replaced by the new ones."
    message "${DEFAULT_COLOR}"
    if query "Do you want to replace /etc/[profile|bashrc] ? " y ; then
      [ -f /etc/profile ] && mv /etc/profile /etc/profile.old
      [ -f /etc/bashrc  ] && mv /etc/bashrc /etc/bashrc.old
      install -m 644 -o root -g root $SCRIPT_DIRECTORY/profile /etc/profile
      install -m 644 -o root -g root $SCRIPT_DIRECTORY/bashrc /etc/bashrc
      message ""
      if query "Do you want root to have the new .bash_* files ? " y ; then
        [ -L /root/.bashrc ] && rm /root/.bashrc
        install -m 600 -o root -g root $SCRIPT_DIRECTORY/skel/.bash_profile /root/.bash_profile
        install -m 600 -o root -g root $SCRIPT_DIRECTORY/skel/.bashrc /root/bashrc
        install -m 600 -o root -g root $SCRIPT_DIRECTORY/skel/.bash_logout /root/.bash_logout
        [ -L /root/.bash_history ] || rm /root/.bash_history
        [ -e /root/.bash_history ] || ln -s /dev/null /root/.bash_history
      fi
      message "${MESSAGE_COLOR}Make sure your users also get the new .bash* from /etc/skel! ${DEFAULT_COLOR}"
    fi
  fi  &&

  if [ ! -e /etc/profile ] ; then
    install -m 644 -o root -g root $SCRIPT_DIRECTORY/profile /etc/profile
  fi  &&
  if [ ! -e /etc/bashrc ] ; then
    install -m 644 -o root -g root $SCRIPT_DIRECTORY/bashrc /etc/bashrc
  fi

) > $C_FIFO 2>&1
