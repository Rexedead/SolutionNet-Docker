# docker run --name some-postgres -p 5432:5432 -e POSTGRES_PASSWORD=pass -v "./sql-setup":/home/ -d postgres
# docker exec -u postgres -it some-postgres /bin/bash
# RUN createdb sdb
# RUN psql -U postgres -d sdb -f /home/dump
FROM postgres
COPY dump /docker-entrypoint-initdb.d/10-init.sql