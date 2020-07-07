FROM node:lts as builder

RUN mkdir /project && \
    cd /project && \
    git clone --depth=1 https://github.com/mobz/elasticsearch-head.git && \
    cd elasticsearch-head && \
    npm install

FROM node:lts-alpine

COPY --from=builder /project /project

WORKDIR /project/elasticsearch-head

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["npm", "run", "start"]
