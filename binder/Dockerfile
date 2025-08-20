FROM jupyter/base-notebook

USER root
RUN apt-get update && apt-get install -y libicu-dev
USER $NB_USER

# Install .NET SDK to jovyan's home directory
RUN wget https://dot.net/v1/dotnet-install.sh \
    && chmod +x dotnet-install.sh \
    && ./dotnet-install.sh -c 7.0 --install-dir /home/jovyan/.dotnet

# Set environment variables for all future layers
ENV DOTNET_ROOT="/home/jovyan/.dotnet"
ENV PATH="/home/jovyan/.dotnet:${PATH}"
ENV PATH="/home/jovyan/.dotnet/tools:${PATH}"

# Install .NET Interactive as a global tool for jovyan
RUN export DOTNET_ROOT="/home/jovyan/.dotnet" && \
    export PATH="/home/jovyan/.dotnet:/home/jovyan/.dotnet/tools:${PATH}" && \
    /home/jovyan/.dotnet/dotnet tool install --global Microsoft.dotnet-interactive --version 1.0.431302 && \
    /home/jovyan/.dotnet/tools/dotnet-interactive jupyter install

WORKDIR /home/jovyan
EXPOSE 8888

COPY . ${HOME}
