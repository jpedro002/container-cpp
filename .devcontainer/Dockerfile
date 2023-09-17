ARG VARIANT=11-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/java:${VARIANT}


ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="${templateOption:reinstallCmakeVersionFromSource}"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/

RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# Instale o OpenJDK (Java)
RUN apt-get update && apt-get install -y openjdk-11-jdk

# Instale o Python 3 e o gerenciador de pacotes pip
RUN apt-get install -y python3 python3-pip

# Instale o compilador C++
RUN apt-get install -y g++

# Defina uma variável de ambiente para o Java
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64

# Crie um diretório para armazenar o código fonte
WORKDIR /app

# Copie seu código-fonte para o contêiner (se necessário)
# COPY ./seu_codigo_c.cpp /app/seu_codigo_c.cpp
# COPY ./seu_codigo_java.java /app/seu_codigo_java.java
# COPY ./seu_codigo_python.py /app/seu_codigo_python.py

# Exemplo: execute o Python por padrão
CMD ["python3", "seu_codigo_python.py"]
