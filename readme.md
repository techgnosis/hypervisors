# Hardware level
* Intel VT-x and AMD-V
  * Creates a new privilege level (root mode) with more access than ring 0. The VMM is in root mode and so it can intercept specific assembly instructions from the guest OS. This allows for the guest OS instructions to be executed on the host except for specific instructions that need to be handled in alternative ways. Before this feature, all CPU execution had to be emulated because you could not safely execute every instruction.
  * Hardware managed memory mapping between host and guest. This was too costly before the hardware acceleration.
* Intel VT-d and AMD-Vi
  * Creates a new hardware component called the IOMMU
  * IOMMU allows for PCI Passthrough

# Kernel level
* Linux KVM
  * /dev/kvm
* Apple Hypervisor Framework (HF)
  * API


# Virtual Machine Managers (VMMs)
Manage CPU and memory, emulate a few key devices, and implement VirtIO backends

* Apple Virtualization Framework (VF) API
  * Apple HF only, obviously
  * Technically an API but its very high level so I'll call it a VMM too
* qemu
  * KVM or Apple HF
* Rust VMM
  * KVM or Apple HF
  * https://github.com/rust-vmm/vm-virtio
  * https://github.com/rust-vmm/kvm
  * https://github.com/cloud-hypervisor/cloud-hypervisor
  * https://github.com/firecracker-microvm/firecracker
  * https://github.com/google/crosvm
* Microsoft OpenVMM
  * KVM and maybe HF, I don't know
  * https://github.com/microsoft/openvmm
  * Written in Rust but does not use Rust VMM


# Tools that use other tools
* lima
  * qemu
  * vz (VF Golang library) https://github.com/Code-Hex/vz
* UTM
  * qemu
  * VF directly (UTM written in Swift)
  * has `utmctl` as well
* Tart
  * https://github.com/cirruslabs/tart
  * tart only supports VF. It is Apple only
  * runs VMs from OCI images
* Lume
  * Part of the Cua project
  * https://github.com/trycua/cua/blob/main/libs/lume/README.md
  * Only supports Apple VF
* libvirt uses a variety of backends
  * https://libvirt.org/manpages/index.html#modular-driver-daemons


# SR-IOV
PCIe and device standard to allow for sharing PCIe devices. It creates multiple Virtual Functions (VFs) from one Physical Function (PF).

# VFIO
Linux kernel feature. Uses the CPUs IOMMU to pass a device to a VM. VFIO can pass a real device or an SR-IOV VF.

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
