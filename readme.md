# CPU and memory virtualization
* Intel VT-x and AMD-V
* Linux KVM
  * /dev/kvm
* Apple Hypervisor Framework (HF) API


# machine virtualization
Use KVM or HF and implement VirtIO backends

* Apple Virtualization Framework (VF) API
* qemu
  * does not use VF on Apple
* Rust VMM
  * https://github.com/rust-vmm/vm-virtio
  * https://github.com/rust-vmm/kvm
  * https://github.com/cloud-hypervisor/cloud-hypervisor
  * https://github.com/firecracker-microvm/firecracker
  * https://github.com/google/crosvm
* Microsoft OpenVMM
  * https://github.com/microsoft/openvmm
  * Written in Rust but does not use Rust VMM


# VM Managers (VMMs)
* lima
  * qemu
  * vz (VF Golang library) https://github.com/Code-Hex/vz
* UTM
  * qemu or VF directly (UTM written in Swift)
  * has `utmctl` as well
* Tart
  * https://github.com/cirruslabs/tart
  * tart only uses VF. It is Apple only
  * runs VMs from OCI images
* Lume
  * Part of the Cua project
  * https://github.com/trycua/cua/blob/main/libs/lume/README.md
* libvirt uses a variety of backends
  * https://libvirt.org/manpages/index.html#modular-driver-daemons


# Paravirtualization and VirtIO
VirtIO is a driver spec. Linux kernel contains one set of VirtIO device driver "frontends". They communicate with the "backends" hosted in the qemu process. This is much less work for qemu than emulating a full device.

# Emulation
There are 4-5 devices that an OS needs to even boot and so these devices can't be paravirtualized and must be truly emulated
* Keyboard controller
* Timer
* Serial port
* Interrupt controllers


# Ignoring
* Windows
* Oracle
* VMWare
* Canonical Multipass
