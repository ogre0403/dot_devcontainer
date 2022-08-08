FROM google/cloud-sdk:latest


RUN apt-get -y install kubectl google-cloud-sdk-gke-gcloud-auth-plugin bash-completion jq wget
RUN curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
RUN wget https://github.com/mikefarah/yq/releases/download/v4.27.2/yq_linux_amd64 -O /usr/bin/yq && \
    chmod +x /usr/bin/yq

# Install krew and useful plugin
RUN set -x; cd "$(mktemp -d)" && \
    OS="$(uname | tr '[:upper:]' '[:lower:]')" && \
    ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" && \
    KREW="krew-${OS}_${ARCH}" && \
    curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" && \
    tar zxvf "${KREW}.tar.gz" && \
    ./"${KREW}" install krew  && \
    ./"${KREW}" install ctx   && \
    ./"${KREW}" install ns    && \
    ./"${KREW}" install neat   
    

# Install kube-ps1
RUN git -C /opt clone https://github.com/jonmosco/kube-ps1.git
    
RUN echo 'export USE_GKE_GCLOUD_AUTH_PLUGIN=True'               >> /root/.bashrc && \
    echo 'source /usr/lib/google-cloud-sdk/completion.bash.inc' >> /root/.bashrc && \
    echo 'source /etc/profile.d/bash_completion.sh'             >> /root/.bashrc && \
    echo 'source <(helm completion bash)'                       >> /root/.bashrc && \
    echo 'source <(kubectl completion bash)'                    >> /root/.bashrc && \
    echo 'export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"'    >> /root/.bashrc && \
    echo 'source /opt/kube-ps1/kube-ps1.sh'                     >> /root/.bashrc && \
    echo "PS1='[\u@\h \W \$(kube_ps1)]\$ '"                     >> /root/.bashrc && \
    echo 'alias k=kubectl'                                      >> /root/.bashrc && \
    echo 'complete -o default -F __start_kubectl k'             >> /root/.bashrc




