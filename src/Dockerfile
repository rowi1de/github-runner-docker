FROM ubuntu

ARG repoName
ARG repoToken

ENV USER=runner
ENV UID=12345
ENV GID=23456

RUN addgroup --gid "$GID" "$USER" && \
    adduser \
    --disabled-password \
    --gecos "" \
    --ingroup "$USER" \
    --uid "$UID" \
    "$USER"


RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y curl 

#Download the latest runner package
RUN mkdir actions-runner
RUN chown runner actions-runner
RUN cd actions-runner
RUN curl -O https://githubassets.azureedge.net/runners/2.160.2/actions-runner-linux-x64-2.160.2.tar.gz
RUN tar xzf ./actions-runner-linux-x64-2.160.2.tar.gz

#Microsoft Owns GitHub
RUN ./bin/installdependencies.sh

RUN touch .path
RUN touch .env
RUN touch /.credentials_rsaparams
RUN mkdir /_diag
RUN chown runner /_diag
RUN chown runner .path
RUN chown runner .env
RUN chown runner /.credentials_rsaparams

USER runner
RUN ./config.sh --url https://github.com/ScaCap/${repoName}} --token ${repoToken}}

CMD ["./run.sh"]