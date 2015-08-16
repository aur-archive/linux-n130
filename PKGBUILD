# Maintainer: DonVla <donvla@users.sourceforge.net>

_do_patch=1
pkgname=linux-n130
_kernelname=-N130
_basekernel=3.9
#pkgver=${_basekernel}
_minrev=.4
pkgver=${_basekernel}${_minrev}
pkgrel=1
pkgdesc="The Linux kernel and modules for SAMSUNG N130 - optionally with Con Kolivas' ck patchset and/or BFQ patches"
arch=('i686')
license=('GPL2')
options=(!strip)
url="http://www.kernel.org"
depends=('coreutils' 'linux-firmware' 'lzop' 'kmod' 'mkinitcpio>=0.7')
install="linux${_kernelname}.install"
backup=("etc/mkinitcpio.d/linux-N130.preset")
_kernel_path="http://www.kernel.org/pub/linux/kernel/v3.x"
_kernel_path="http://ftp.halifax.rwth-aachen.de/kernel/linux/kernel/v3.x"
_patchname="patch-${_basekernel}${_minrev}"
# http://users.on.net/~ckolivas/kernel/
_ck_patchver=ck1
#_ck_path="http://www.kernel.org/pub/linux/kernel/people/ck/patches/3.0/${_basekernel}/${_basekernel}.0-${_ck_patchver}"
_ck_path="http://ck.kolivas.org/patches/"
#_ck_path="http://repo-ck.com/source/${_ck_patchver}"
#_ck_patch_path="3.0/${_basekernel}/${_basekernel}-${_ck_patchver}"
_ck_patch_path="3.0/${_basekernel}/${_basekernel}-${_ck_patchver}"
_ck_patchname="patch-${_basekernel}-${_ck_patchver}"
_ck_bfs_path="/bfs/3.0/${_basekernel}/"
#_ck_bfs_patchname="${_basekernel}-bfs426-427.patch"
_bfq_ver="v6r1"
_bfq_path="http://algo.ing.unimo.it/people/paolo/disk_sched/patches/${_basekernel}.0-${_bfq_ver}"
source=("${_kernel_path}/linux-${_basekernel}.tar.bz2"
        "${_kernel_path}/${_patchname}.bz2"
        "${_ck_path}/${_ck_patch_path}/${_ck_patchname}.bz2"
        # "${_ck_path}/${_ck_bfs_path}/${_ck_bfs_patchname}"
        "config" "mkinitcpio-N130.conf" "linux-N130.preset"
        logo_linux_{clut224.ppm,mono.pbm,vga16.ppm}
        "change-default-console-loglevel.patch"
        "${_bfq_path}/0001-block-cgroups-kconfig-build-bits-for-BFQ-${_bfq_ver}-${_basekernel}.patch"
        "${_bfq_path}/0002-block-introduce-the-BFQ-${_bfq_ver}-I-O-sched-for-${_basekernel}.patch" )
optdepends=('crda: to set the correct wireless channels of your country')
md5sums=('2220321a0a14d86200322e51dd5033e2'
         'c0f20f2c33265b128610d735cb344e9a'
         '1268369beeeffc0ed6c1bba3973d3fba'
         '2733d1d053278f828bdee524b7809343'
         'bfdcb2a4be0152282d0b2803c89644f7'
         '6c44c7be508b5de9ae00533fead51ff6'
         '6a5a1925501fe20fafd04fdb3cb4f6ed'
         'e8c333eaeac43f5c6a1d7b2f47af12e2'
         'c120adbd9c0daa0136237a83adeabd1e'
         '9d3c56a4b999c8bfbd4018089a62f662'
         '62dff7101a1381d33faf2e1f101ba684'
         '2c719719165dccf5fc52705e59797d26')
sha256sums=('97e48f31ed2197f4e7e4938d4fab8da522cf80e60c6ce69668b0805904499305'
            '3d48936f2b20ddf95131ddf494df068788a87b49fb47e9a68efdf7f3a2cac319'
            '0fc088cacfbac2cda9081aba506f152cff811f1578bceafdab3a82adda415e25'
            'bdf6a785dca79d00ea72981a21ffa6d6165700bff5cf45624a077ddc2f6f9d9f'
            '8e66344ccee4b9d41435aba32414a9ac34e92ff68b2cb1faa67f75fc26a22533'
            'ed4d88380a4a70a460215cc444727fb5f90d8b10b5e899de9d5d24890efbf36c'
            '4274579ccf42a9acc03283edffea2dda2c4a48e3fd734bbaeada4c16dff9d156'
            '1e5bea8de1c2cc24498fb9a4fdbb313f36f38f671f2bfc46ccf7acbd7958a4b9'
            'f9c7c1275313890fc12f6bab92e2c0794b5041e223d868eb0e34cd99baee3d7a'
            'b9d79ca33b0b51ff4f6976b7cd6dbb0b624ebf4fbf440222217f8ffc50445de4'
            'ec99a25471dddd6c860762ab3895f94c07181e25f5d4785c66422fff8328cf40'
            '53a4db3514254fb4ef7c6232e1b6aa2c82818df89660fe16f772b472bff332f1')

build() {
  # change to 1 (or else) if you want to use the BF scheduler
  # http://users.on.net/~ckolivas/kernel/
  _USE_CK_PATCHSET=1
  # change to 1 (or else) if you want to use the BFQ i/o scheduler
  # http://algo.ing.unimo.it/people/paolo/disk_sched/
  _USE_BFQ_PATCHES=1
  # default resume partition -> your swap partition. eg: 
  #_RESUME_SWAP_PARTITION="/dev/sda3"
  # NO PERSISTENT NAMING! If in doubt, leave it empty
  _RESUME_SWAP_PARTITION=""

  cd "${srcdir}/linux-${_basekernel}"

  # Add revision patches
  (( _do_patch )) && [[ ! -z "${_minrev}" ]] && msg "Adding revision patches..." && (patch -Np1 < "${srcdir}/${_patchname}")

  # Add Arch Linux logo to the source
  msg "Adding Arch Linux logo..."
  install -v -m 0644 "${srcdir}/logo_linux_clut224.ppm"  drivers/video/logo/logo_linux_clut224.ppm &&
  install -v -m 0644 "${srcdir}/logo_linux_mono.pbm"     drivers/video/logo/logo_linux_mono.pbm &&
  install -v -m 0644 "${srcdir}/logo_linux_vga16.ppm"    drivers/video/logo/logo_linux_vga16.ppm

  ###
  ### Arch stock kernel patches
  #
  (( _do_patch )) && patch -Np1 -i "${srcdir}/change-default-console-loglevel.patch"

  ###
  ### Additional linux-N130 patches
  # 
  # Add CK's BFS patch
  if (( _do_patch && _USE_CK_PATCHSET )); then 
    msg "Adding CK patchset..." 
    patch -Np1 < "${srcdir}/${_ck_patchname}"
    #patch -Np1 < "${srcdir}/${_ck_bfs_patchname}"
  fi

  if (( _do_patch && _USE_BFQ_PATCHES )); then
    msg "Adding BFQ patches..."
    local _patch
    for _patch in "${srcdir}"/000*-block-*.patch; do
        patch -Np1 < "${_patch}"
    done 
  fi

  # Copy config
  cat ../config > ./.config
  # set swap partition for resuming - no resume= kernel line needed
  if [[ "${_RESUME_SWAP_PARTITION}" ]]; then 
    sed -e "s|CONFIG_PM_STD_PARTITION=.*|CONFIG_PM_STD_PARTITION=\""${_RESUME_SWAP_PARTITION}"\"|g" -i ./.config
  fi

  sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"${_kernelname}\"|g" ./.config

  # set extraversion to pkgrel
  #sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

  # Remove EXTRAVERSION from Makefile. Version will remain ${pkgver}-${pkgrel}-${_kernelname}
  sed -e "s|^EXTRAVERSION\ .*|EXTRAVERSION\ = "-${pkgrel}"|g" -i Makefile
  
  # remove the sublevel from Makefile
  # this ensures our kernel version is always 3.X-ARCH
  # this way, minor kernel updates will not break external modules
  # we need to change this soon, see FS#16702
  #sed -ri 's|^(SUBLEVEL =).*|\1|' Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh

  # get kernel version
  make prepare
  ####################
  ###
  ### Configure the kernel and stop afterwards
  ### this is useful to configure the kernel
  #make oldconfig
  ###
  ### This one also moves the config file to ${startdir} for later use. 
  ### Don't forget to rebuild the checksums afterwards! 
  #make menuconfig && cp -v .config ${startdir}/config && \
  #msg "Stopping build." && msg "Config file is copied to startdir. Don't forget to rebuild checksums!" && return 1
  ### new nconfig
  #make nconfig && cp -v .config ${startdir}/config && \
  #msg "Stopping build." && msg "Config file is copied to startdir. Don't forget to rebuild checksums!" && return 1
  ####################
  yes "" | make config
  # build!
  make ${MAKEFLAGS} bzImage modules
}

package() {
  KARCH=x86

  cd "${srcdir}/linux-${_basekernel}"
  # Get kernel version  
  _kernver="$(make kernelrelease)"

  ###
  ### install kernel and modules (kernel package)
  ###
  mkdir -p "${pkgdir}"/{lib/modules,lib/firmware,boot}
  make INSTALL_MOD_PATH="${pkgdir}" modules_install
  cp arch/${KARCH}/boot/bzImage ${pkgdir}/boot/vmlinuz${_kernelname}

  # add vmlinux
  install -m644 -D vmlinux ${pkgdir}/usr/src/linux-${_kernver}/vmlinux

  # install N130 mkinitcpio.conf and preset file for kernel
  install -m644 -D ${srcdir}/mkinitcpio-N130.conf ${pkgdir}/etc/mkinitcpio-N130.conf
  install -m644 -D ${srcdir}/linux${_kernelname}.preset ${pkgdir}/etc/mkinitcpio.d/linux${_kernelname}.preset

  # set correct depmod command for install
  sed \
    -e  "s/KERNEL_NAME=.*/KERNEL_NAME=${_kernelname}/g" \
    -e  "s/KERNEL_VERSION=.*/KERNEL_VERSION=${_kernver}/g" \
    -i "${startdir}/linux${_kernelname}.install"

  sed \
    -e "s|ALL_kver=.*|ALL_kver=\"/boot/vmlinuz${_kernelname}\"|g" \
    -e "s|default_image=.*|default_image=\"/boot/linux${_kernelname}.img\"|g" \
    -e "s|fallback_image=.*|fallback_image=\"/boot/initramfs${_kernelname}-fallback.img\"|g" \
    -i ${pkgdir}/etc/mkinitcpio.d/linux${_kernelname}.preset

  # remove build and source links
  rm -f "${pkgdir}/lib/modules/${_kernver}"/{source,build}
  # remove the firmware
  rm -rf "${pkgdir}/lib/firmware"
  # gzip -9 all modules to safe 100MB of space
  find "$pkgdir" -name '*.ko' -exec gzip -9 {} \;

  # add real version for building modules and running depmod from post_install/upgrade
  mkdir -p "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname}"
  echo "${_kernver}" > "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname}/version"
  # make room for external modules
  ln -s "../extramodules-${_basekernel}${_kernelname}" "${pkgdir}/lib/modules/${_kernver}/extramodules"

  # Now we call depmod...
  depmod -b "$pkgdir" -F System.map "$_kernver"

  # move module tree /lib -> /usr/lib
  mv "$pkgdir/lib" "$pkgdir/usr"

  ###
  ### install kernel headers (kernel headers package)
  ###
  #mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}"
  cd "${pkgdir}/usr/lib/modules/${_kernver}" && ln -sf ../../../src/linux-${_kernver} build

  cd "${srcdir}/linux-${_basekernel}"
  install -D -m644 Makefile "${pkgdir}/usr/src/linux-${_kernver}/Makefile"
  install -D -m644 kernel/Makefile "${pkgdir}/usr/src/linux-${_kernver}/kernel/Makefile"
  install -D -m644 .config "${pkgdir}/usr/src/linux-${_kernver}/.config"

  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/include"
  for i in acpi asm-generic config crypto drm generated linux math-emu media net pcmcia scsi sound trace uapi video xen; do
    cp -a include/${i} "${pkgdir}/usr/src/linux-${_kernver}/include/"
  done

  # copy arch includes for external modules
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/arch/x86"
  cp -a arch/x86/include "${pkgdir}/usr/src/linux-${_kernver}/arch/x86/"

  # copy files necessary for later builds, like nvidia and vmware
  cp Module.symvers "${pkgdir}/usr/src/linux-${_kernver}"
  cp -a scripts "${pkgdir}/usr/src/linux-${_kernver}"

  # fix permissions on scripts dir
  chmod og-w -R ${pkgdir}/usr/src/linux-${_kernver}/scripts
  mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/.tmp_versions

  mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/arch/$KARCH/kernel

  cp arch/$KARCH/Makefile ${pkgdir}/usr/src/linux-${_kernver}/arch/$KARCH/
  cp arch/$KARCH/Makefile_32.cpu ${pkgdir}/usr/src/linux-${_kernver}/arch/$KARCH/
  cp arch/$KARCH/kernel/asm-offsets.s ${pkgdir}/usr/src/linux-${_kernver}/arch/$KARCH/kernel/

  # add docbook makefile
  install -D -m644 Documentation/DocBook/Makefile \
    "${pkgdir}/usr/src/linux-${_kernver}/Documentation/DocBook/Makefile"

  # add headers for lirc package
  # pci
  for i in bt8xx cx88 saa7134; do
    mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/pci/${i}"
    cp -a drivers/media/pci/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/pci/${i}"
  done
  # usb
  for i in cpia2 em28xx pwc sn9c102; do
    mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/${i}"
    cp -a drivers/media/usb/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/${i}"
  done
  # i2c
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c"
  cp drivers/media/i2c/*.h  "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/"
  for i in cx25840; do
    mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/${i}"
    cp -a drivers/media/i2c/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/${i}"
  done

  # add dm headers
  mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/drivers/md
  cp drivers/md/*.h  ${pkgdir}/usr/src/linux-${_kernver}/drivers/md
  
  # add inotify.h
  mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/include/linux
  cp include/linux/inotify.h ${pkgdir}/usr/src/linux-${_kernver}/include/linux/
  # add wireless headers
  mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/net/mac80211/
  cp net/mac80211/*.h ${pkgdir}/usr/src/linux-${_kernver}/net/mac80211/

  # add dvb headers for external modules
  # in reference to:
  # http://bugs.archlinux.org/task/9912
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-core"
  cp drivers/media/dvb-core/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-core/"
  # and...
  # http://bugs.archlinux.org/task/11194
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/include/config/dvb/"
  cp include/config/dvb/*.h "${pkgdir}/usr/src/linux-${_kernver}/include/config/dvb/"

  # add dvb headers for http://mcentral.de/hg/~mrec/em28xx-new
  # in reference to:
  # http://bugs.archlinux.org/task/13146
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
  cp drivers/media/dvb-frontends/lgdt330x.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
  cp drivers/media/i2c/msp3400-driver.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/"

  # add dvb headers
  # in reference to:
  # http://bugs.archlinux.org/task/20402
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/dvb-usb"
  cp drivers/media/usb/dvb-usb/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/dvb-usb/"
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends"
  cp drivers/media/dvb-frontends/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/tuners"
  cp drivers/media/tuners/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/tuners/"

  # add xfs and shmem for aufs building
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/fs/xfs"
  mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/mm"
  cp fs/xfs/xfs_sb.h "${pkgdir}/usr/src/linux-${_kernver}/fs/xfs/xfs_sb.h"

  # copy in Kconfig files
  for i in `find . -name "Kconfig*"`; do 
    mkdir -p ${pkgdir}/usr/src/linux-${_kernver}/`echo $i | sed 's|/Kconfig.*||'`
    cp $i ${pkgdir}/usr/src/linux-${_kernver}/$i
  done

  chown -R root.root ${pkgdir}/usr/src/linux-${_kernver}
  find ${pkgdir}/usr/src/linux-${_kernver} -type d -exec chmod 755 {} \;

  # strip scripts directory
  find ${pkgdir}/usr/src/linux-${_kernver}/scripts  -type f -perm -u+w 2>/dev/null | while read binary ; do
    case "$(file -bi "$binary")" in
      *application/x-sharedlib*) # Libraries (.so)
        /usr/bin/strip $STRIP_SHARED "$binary";;
      *application/x-archive*) # Libraries (.a)
        /usr/bin/strip $STRIP_STATIC "$binary";;
      *application/x-executable*) # Binaries
        /usr/bin/strip $STRIP_BINARIES "$binary";;
    esac 
  done 

  # remove unneeded architectures
  rm -rf "${pkgdir}/usr/src/linux-${_kernver}/arch"/{alpha,arm,arm26,avr32,blackfin,cris,frv,h8300,ia64,m32r,m68k,m68knommu,mips,microblaze,mn10300,parisc,powerpc,ppc,s390,sh,sh64,sparc,sparc64,um,v850,xtensa}
}
