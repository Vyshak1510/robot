FROM node:14

ENV INSTANA_AUTO_PROFILE true
ENV NEW_RELIC_NO_CONFIG_FILE=true

EXPOSE 8080

WORKDIR /opt/server

COPY package.json /opt/server/
# COPY --from=fzf53242.live.dynatrace.com/linux/oneagent-codemodules:nodejs / /
# ENV LD_PRELOAD /opt/dynatrace/oneagent/agent/lib64/liboneagentproc.so
ENV NEW_RELIC_DISTRIBUTED_TRACING_ENABLED=true \
NEW_RELIC_LOG=stdout
# etc.

RUN npm install

COPY server.js /opt/server/

CMD ["node", "server.js"]

