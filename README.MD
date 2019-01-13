To Trigger update 
# eval $(sudo ../kubernetes/minikube-linux-amd64 docker-env) \
  && cd roles/build-air-ports/s2i/airports-assembly/ \
  && sed -i s/airports-assembly-1.0.1.jar/airports-assembly-1.1.0.jar/g Dockerfile \
  && docker build -t airports-assembly:1.1.0 . \
  && sudo kubectl set image deployment airports-assembly airports-assembly=airports-assembly:1.1.0 --record -n airports && cd -
