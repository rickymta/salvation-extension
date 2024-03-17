# Dump build stage
FROM postgres:16.2-alpine3.19 as dumper

# Copy script file
COPY ../scripts/inititalize.sql /docker-entrypoint-initdb.d/

RUN ["sed", "-i", "s/exec \"$@\"/echo \"skipping...\"/", "/usr/local/bin/docker-entrypoint.sh"]

# Environment
ENV POSTGRES_DB=postgres
ENV POSTGRES_USER=postgres
ENV POSTGRES_PASSWORD=postgres
ENV PGDATA=/data

RUN ["/usr/local/bin/docker-entrypoint.sh", "postgres"]

# Final build stage
FROM postgres:16.2-alpine3.19

COPY --from=dumper /data $PGDATA

# Expose port
EXPOSE 5432
