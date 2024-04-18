FROM gradle:jdk17

ENV NODE_VERSION 20.12.2
ENV NVM_DIR /usr/local/nvm
ENV ANDROID_HOME /opt/android-sdk

# Create NVM directory
RUN mkdir -p $NVM_DIR

# Install NVM & NODE
# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash \
    && chmod +x $NVM_DIR/nvm.sh
# && export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" \
# && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
# && nvm -v \
# && nvm install ${NODE_VERSION} \
# && nvm use ${NODE_VERSION}

RUN bash -c "source $NVM_DIR/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    chmod -R 777 $NVM_DIR"


# Set node and npm environment variables
ENV PATH $NVM_DIR/versions/node/v${NODE_VERSION}/bin:$PATH
# Set PATH to include NVM directory
ENV PATH $NVM_DIR:$PATH

# Display Node.js version
RUN node --version
RUN npm --version

# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #
# -------------------------------------------------------------------------------------- #

# INSTALL ANDROID COMMAND LINE TOOLS
RUN rm -rf ${ANDROID_HOME} \
    &&  mkdir -p ${ANDROID_HOME}

WORKDIR ${ANDROID_HOME}
RUN curl -sL https://dl.google.com/android/repository/commandlinetools-linux-7302050_latest.zip -o android-sdk-tools.zip \
    && unzip -q android-sdk-tools.zip -d ${ANDROID_HOME} \
    && rm -f android-sdk-tools.zip 
WORKDIR ${ANDROID_HOME}/cmdline-tools
RUN mkdir -p latest
RUN mv NOTICE.txt bin lib source.properties latest
RUN ls -l
RUN yes | ${ANDROID_HOME}/cmdline-tools/latest/bin/sdkmanager --licenses


# INSTALL YARN
RUN npm install --global yarn
RUN yarn --version


CMD ["/bin/sh"]