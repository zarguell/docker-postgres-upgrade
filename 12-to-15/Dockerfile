FROM postgres:15-bullseye

RUN sed -i 's/$/ 12/' /etc/apt/sources.list.d/pgdg.list

RUN apt-get update && apt-get install -y --no-install-recommends \
		postgresql-12=12.12-1.pgdg110+1 \
	&& rm -rf /var/lib/apt/lists/*

ENV PGBINOLD /usr/lib/postgresql/12/bin
ENV PGBINNEW /usr/lib/postgresql/15/bin

ENV PGDATAOLD /var/lib/postgresql/12/data
ENV PGDATANEW /var/lib/postgresql/15/data

RUN mkdir -p "$PGDATAOLD" "$PGDATANEW" \
	&& chown -R postgres:postgres /var/lib/postgresql

WORKDIR /var/lib/postgresql

COPY docker-upgrade /usr/local/bin/

ENTRYPOINT ["docker-upgrade"]

# recommended: --link
CMD ["pg_upgrade"]
