Vagrant.configure("2") do |config|
  config.vm.define "KubernetesPractice" do |node|
    node.vm.box = "ubuntu/focal64"
    
    # Configuración del teclado en español
    node.vm.provision "shell", inline: "sudo localectl set-keymap es"

    node.vm.provider "virtualbox" do |vb|
      vb.name = "KubernetesPractice"
      vb.memory = "2048"
      vb.cpus = "2"
    end

    node.vm.provision "shell", inline: <<-SHELL
      # Actualizar repositorios
      sudo apt-get update
      
      # Instalar Docker
      sudo apt-get install -y docker.io

      # Agregar el usuario vagrant al grupo docker
      sudo usermod -aG docker vagrant

      # Instalar Minikube
      curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

      # Instalar kubectl
      sudo apt-get install -y kubectl

      # Instalar Kubernetes
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
      sudo apt-get update
      sudo apt-get install -y kubelet kubeadm kubectl
    SHELL
  end
end
