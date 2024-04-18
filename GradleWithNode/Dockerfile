FROM gradle:jdk17

ENV NODE_VERSION 20.12.2
ENV NVM_DIR /root/.nvm

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash \
    && export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && nvm -v \
    && nvm install ${NODE_VERSION} \
    && nvm use ${NODE_VERSION}

RUN echo "Test"
RUN echo "source $NVM_DIR/nvm.sh" >> /root/.bashrc
RUN echo $NVM_DIR

# Set node and npm environment variables
ENV NODE_PATH $NVM_DIR/v${NODE_VERSION}/lib/node_modules
# ENV PATH $NVM_DIR/versions/node/v${NODE_VERSION}/bin:$PATH

# Modify the shell initialization file to source nvm.sh
RUN echo "source /root/.nvm/nvm.sh" >> /root/.profile

CMD ["/bin/sh"]