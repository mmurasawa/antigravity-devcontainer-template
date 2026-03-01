FROM rockylinux/rockylinux:10

RUN dnf install -y \
    git \
    which \ 
    wget \
    procps \
    openssh-clients \
    && dnf clean all

    # vscode ユーザー
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

WORKDIR /workspace

# vscode user に切り替え
USER vscode

# (optional) node install
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash && \
    \. "$HOME/.nvm/nvm.sh" && \
    nvm install 24

# (optional) python install with uv and default
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    \. "$HOME/.local/bin/env" && \
    uv python install 3.14.3 --default

# run forever to keep the container alive
CMD ["sleep", "infinity"]
