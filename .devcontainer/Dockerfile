FROM alpine:3.20

ARG KIND_VERSION=0.14.0

RUN apk add --no-cache \
    bash ca-certificates curl git docker-cli \
    openssh

# sshd runtime setup
RUN mkdir -p /var/run/sshd \
 && ssh-keygen -A \
 && sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config \
 && sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config

# kubectl
RUN curl -fsSL -o /usr/local/bin/kubectl \
    "https://dl.k8s.io/release/$(curl -fsSL https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
 && chmod +x /usr/local/bin/kubectl

# kind
RUN curl -fsSL -o /usr/local/bin/kind \
    "https://github.com/kubernetes-sigs/kind/releases/download/v${KIND_VERSION}/kind-linux-amd64" \
 && chmod +x /usr/local/bin/kind

CMD ["/usr/sbin/sshd","-D","-e"]
