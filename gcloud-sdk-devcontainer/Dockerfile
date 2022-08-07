FROM google/cloud-sdk:alpine

RUN gcloud components install kubectl gke-gcloud-auth-plugin
RUN apk add openssl bash-completion 
RUN bash <(curl -s https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3) 

RUN echo 'export USE_GKE_GCLOUD_AUTH_PLUGIN=True'       >> /root/.bashrc && \
    echo 'source /google-cloud-sdk/completion.bash.inc' >> /root/.bashrc && \
    echo 'source /etc/profile.d/bash_completion.sh'     >> /root/.bashrc && \
    echo 'source <(helm completion bash)'               >> /root/.bashrc && \
    echo 'source <(kubectl completion bash)'            >> /root/.bashrc



