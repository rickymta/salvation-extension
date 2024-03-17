# Arguments
ARG PG_VERSION
ARG PG_DATABASE
ARG PG_USER
ARG PG_PASSWORD

# Dump build stage
FROM postgres:PG_VERSION as dumper

# Copy script file
COPY ../scripts/inititalize.sql /docker-entrypoint-initdb.d/

RUN ["sed", "-i", "s/exec \"$@\"/echo \"skipping...\"/", "/usr/local/bin/docker-entrypoint.sh"]

# Final build stage
FROM postgres:11-alpine

COPY --from=dumper /data $PGDATA

# Environment
ENV POSTGRES_DB=PG_DATABASE
ENV POSTGRES_USER=PG_USER
ENV POSTGRES_PASSWORD=PG_PASSWORD

# Expose port
EXPOSE 5432
