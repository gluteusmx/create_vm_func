function create_vm {
    if [ "$1" == "-h" ] || [ -z "$(sudo virsh list --all --name | grep "^$1_template")" ] || [ -z "$2" ]; then
        echo "Usage: $FUNCNAME DISTRO VMNAME"
        echo "Example: $FUNCNAME centos8 student"
        echo "All available DISTRO's: $(sudo virsh list --all --name | grep template | awk -F '_' '{print $1}' | tr '\n' ',')"
        return 0
    fi

    sudo virt-clone -o "$1"_template -n "$2" -f "/var/lib/libvirt/images/$2.qcow2" --connect qemu:///system
    if [ "$?" -ne "0" ]; then
        echo "Failed to clone the virtual machine."
        return 2
    fi

    sudo virt-sysprep -d "$2" --connect qemu:///system
    sudo virsh start --domain "$2"
    if [ "$?" -ne "0" ]; then
        echo "Failed to start the virtual machine."
        return 2
    fi

    echo "Your VM is created and booting up, please wait until it finishes."
    sleep 15

    ip=$(sudo virsh domifaddr "$2" | grep ipv4 | awk '{print $4}' | awk -F '/' '{print $1}')
    echo "IP of your machine is: $ip"
    echo "Try to connect via SSH with:"
    echo "User: root\\student"
    echo "Password: 1\\student"
    echo "Example: ssh root@$ip"
    echo "Password: 1"
}
