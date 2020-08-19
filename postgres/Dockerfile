FROM postgres

COPY create-multiple-postgresql-databases.sh /docker-entrypoint-initdb.d/

# Environment Variables
ENV POSTGRES_USER 'frepple'
ENV POSTGRES_PASSWORD 'frepple'
ENV POSTGRES_MULTIPLE_DATABASES "freppledb","scenario1","scenario2","scenario3"

# Expose port
EXPOSE 5432
