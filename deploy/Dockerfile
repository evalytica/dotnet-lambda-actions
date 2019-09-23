FROM microsoft/dotnet:2.1.500-sdk

LABEL "com.github.actions.name"="dotnet lambda deploy"
LABEL "com.github.actions.description"="Run dotnet lambda deploy"
LABEL "com.github.actions.icon"="play-circle"
LABEL "com.github.actions.color"="purple"

LABEL "repository"="https://github.com/evalytica/dotnet-lambda-actions"
LABEL "homepage"="https://github.com/evalytica/dotnet-lambda-actions"
LABEL "maintainer"="Evalytica DevOps Team <evalytica@veradigmhealth.com>"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      groff \
      jq \
      python \
      python3-pip \
      python3-setuptools \
      zip \
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install awscli

RUN dotnet tool install -g Amazon.Lambda.Tools

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
