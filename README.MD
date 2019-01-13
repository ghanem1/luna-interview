**prerequisites:**
  - Ubuntu 16.04 64bit
  - Recent version of ansible installed.
  - Passwordless execution of sudo commands.

**This playbooks helps to run the whole stack using one command as the following:**
  1. Deploy Kubernetes Cluster on a local machine. (This include minikube and kubectl tools)
  2. Build airports-assembly Docker Image.
  3. Build countries-assembly Docker Image.
  4. Buld nginx Docker Image.
  5. Create NameSpace and trigger deployment for airports-assembly.
  6. Create NameSpace and trigger deployment for countries-assembly.
  7. Create NameSpace and trigger deployment for nginx and expose the service on externalIP

**To Deploy the stack on a local machine:**
  1. Pull this repo into the local machine.
     ```
       git clone https://github.com/ghanem1/luna-interview.git
     ```
  2. Naviage to the downloaded folder and trigger the playbook 
     ```
       cd luna-interview/
       ansible-playbook -i Inventory deploy.yml
     ```
   3. Once the playbook execution gets completed, nginx sevice should have an externalIP than can be used to forward 
      the requests to provided services. (As it is local machine, there is no real public IP. So we are just relying 
      on VM IP )
      ```
        sudo kubectl get svc  -n nginx
      ```

**Later During the interview, it is needed to update airports-assembly to a hgiher version.**
In Real world, this is automated using gitlab CI/DC. However, CI/CD is not configured as this is local cluster.
Following command will be used to trigger the application deployment with 0 down-time.

```
  eval $(sudo ../kubernetes/minikube-linux-amd64 docker-env) \
  && cd roles/build-air-ports/s2i/airports-assembly/ \
  && sed -i s/airports-assembly-1.0.1.jar/airports-assembly-1.1.0.jar/g Dockerfile \
  && docker build -t airports-assembly:1.1.0 . \
  && sudo kubectl set image deployment airports-assembly airports-assembly=airports-assembly:1.1.0 --record -n airports && cd -
```

For any concerns/issues, please contact ghanemdaghstani@gmail.com 
