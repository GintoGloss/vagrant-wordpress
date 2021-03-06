Vagrant.configure("2") do |config|
  N = 2

  VAGRANT_VM_PROVIDER = "virtualbox"
  ANSIBLE_RAW_SSH_ARGS = []

  (1..N-1).each do |machine_id|
    ANSIBLE_RAW_SSH_ARGS << "-o IdentityFile=.vagrant/machines/machine#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  end

  (1..N).each do |machine_id|
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.box = "ubuntu/xenial64"
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "172.29.1.#{10+machine_id-1}"
      machine.vm.network "forwarded_port", guest: 80, host: "#{8080+machine_id}", protocol: "tcp"

      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.become = true
          ansible.playbook = "playbook.yml"
          ansible.groups = {
             "WebServer" => ["machine1"],
             "DbServer" => ["machine2"],
          }

          ansible.verbose = "-v"
          ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
        end
      end
    end
  end
end
