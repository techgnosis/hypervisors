# CPU and memory virtualization
* Intel VT-x and AMD-V
* Linux KVM
  * /dev/kvm
* Apple Hypervisor Framework API



# machine virtualization
* Apple Virtualization Framework (VF)
* qemu
  * does not use VF on Apple
* https://github.com/rust-vmm/kvm
  * https://github.com/cloud-hypervisor/cloud-hypervisor
  * https://github.com/firecracker-microvm/firecracker
  * https://github.com/google/crosvm


# VM Managers (VMMs)
* lima uses qemu or vz (VF Golang library)
* UTM uses qemu or VF directly (UTM written in Swift)
* libvirt uses a variety of backends
  * https://libvirt.org/manpages/index.html#modular-driver-daemons
