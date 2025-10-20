# Linux path
* KVM emulates CPU and memory
* Accessed via /dev/kvm
* Access to CPU virtualization extensions
* qemu uses KVM and emulates devices
* either use qemu or a VMM that uses qemu

# apple
* apple hypervisor framework emulates CPU and memory. KVM parallel
* apple virtualization framework uses the hypervisor framework
* VMM use virtualization framework
* qemu uses its own devices and not VF


# VMMs
* qemu uses KVM or VF
* intel cloud hypervisor uses KVM
* https://github.com/google/crosvm uses KVM
* lima uses qemu or vz, which uses VF
* UTM uses VF or qemu
