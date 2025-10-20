# Hardware level
* Intel VT-x and AMD-V
  * Creates a new privilege level (root mode) with more access than ring 0. The VMM is in root mode and so it can intercept specific assembly instructions from the guest OS. This allows for the guest OS instructions to be executed on the host CPU except for specific instructions that can only be safely handled in alternative ways. Before this feature, all CPU execution had to be emulated because you could not safely execute every instruction.
  * Hardware managed memory mapping between host and guest. This was too costly before the hardware acceleration.
* Intel VT-d and AMD-Vi
  * Creates a new hardware component called the IOMMU
  * IOMMU manages memory mapping between a host PCIe device and a guest OS

# Kernel level
* Linux KVM
  * /dev/kvm via ioctls
* Apple Hypervisor Framework (HF)
  * API


# Hypervisors
Manage CPU and memory, emulate a few key devices, and implement VirtIO backends

* Apple Virtualization Framework (VF) API
  * Apple HF only, obviously
  * Technically an API but its very high level so I'll call it a hypervisor too
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


# Virtual Machine Managers (VMMs)
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
PCIe standard to allow for sharing devices. It creates multiple Virtual Functions (VFs) from one Physical Function (PF). This is useful for saturating high-bandwidth devices like NICs and GPUs, as well as being more streamlined than traditional full device passthrough.

# VFIO
Linux kernel feature. Uses the CPU IOMMU to safely pass device memory to a guest kernel. VFIO can pass a real device or an SR-IOV VF.

# Paravirtualization and VirtIO
VirtIO is a driver spec. Linux kernel contains one set of VirtIO device driver "frontends". They communicate with the "backends" hosted in the hypervisor process and is much less work than emulating a full device.

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
