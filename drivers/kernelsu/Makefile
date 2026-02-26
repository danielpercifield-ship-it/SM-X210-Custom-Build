# 1. Objects to build
obj-y := kernel/ksu.o allowlist.o apk_sign.o app_profile.o extras.o \
         feature.o file_wrapper.o kernel_compat.o kernel_umount.o \
         ksud.o lsm_hooks.o seccomp_cache.o setuid_hook.o \
         su_mount_ns.o sucompat.o supercalls.o throne_tracker.o \
         tiny_sulog.o util.o

# Recursive build for the selinux folder
obj-y += selinux/


# 2. Fix the flask.h and include paths
# This tells the compiler where to find the kernel's own SELinux headers
ccflags-y += -I$(srctree)/security/selinux/include
ccflags-y += -I$(srctree)/$(src)/kernel
ccflags-y += -I$(srctree)/$(src)/selinux

# 3. Critical Flags
ccflags-y += -DCONFIG_KSU_NEXT_MANUAL_HOOK
ccflags-y += -Wno-strict-prototypes -Wno-implicit-function-declaration

# 4. THE V2 SIGNATURE (The Handshake)
# Hardcoding these prevents shell escaping issues in the .yml
KSU_EXPECTED_SIZE := 0x3e6
KSU_EXPECTED_HASH := 79e590113c4c4c0c222978e413a5faa801666957b1212a328e46c00c69821bf7

ccflags-y += -DKSU_NEXT_EXPECTED_SIZE=$(KSU_EXPECTED_SIZE)
ccflags-y += -DKSU_NEXT_EXPECTED_HASH=\"$(KSU_EXPECTED_HASH)\"
