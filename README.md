
# Containerized python and postgres application

## Description
The stack has 2 Docker images which contain the python app and the postgres db respectivly. The docker compose lets the 2 containers interact while the app dockerfile has the right username,password, and db address otherwise you will get an error. The python app runs 3 postgrest sql statements that output a json including details about "total_trips", "avg_fare_by_city", "top_3_cities_by_fare".

## Executing Program
### Run the following in the same location as the docker compose

```
$ make 
$ docker compose up 
```
### Example output (copy/paste)

```
make
docker compose build app
[+] Building 1.0s (11/11) FINISHED                                                                                                                                                                            
 => [internal] load local bake definitions                                                                                                                                                               0.0s
 => => reading from stdin 955B                                                                                                                                                                           0.0s
 => [internal] load build definition from Dockerfile                                                                                                                                                     0.0s
 => => transferring dockerfile: 174B                                                                                                                                                                     0.0s
 => [internal] load metadata for docker.io/library/python:3.11-slim                                                                                                                                      0.5s
 => [internal] load .dockerignore                                                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                                                          0.0s
 => [1/4] FROM docker.io/library/python:3.11-slim@sha256:91e9d01cf4bd56be7128c603506b6fe367ef7506f9f2ad8f3a908aeec8941bb9                                                                                0.0s
 => => resolve docker.io/library/python:3.11-slim@sha256:91e9d01cf4bd56be7128c603506b6fe367ef7506f9f2ad8f3a908aeec8941bb9                                                                                0.0s
 => [internal] load build context                                                                                                                                                                        0.0s
 => => transferring context: 29B                                                                                                                                                                         0.0s
 => CACHED [2/4] RUN pip install --no-cache-dir psycopg[binary]==3.1.19                                                                                                                                  0.0s
 => CACHED [3/4] WORKDIR /app                                                                                                                                                                            0.0s
 => CACHED [4/4] COPY main.py /app/                                                                                                                                                                      0.0s
 => exporting to image                                                                                                                                                                                   0.1s
 => => exporting layers                                                                                                                                                                                  0.0s
 => => exporting manifest sha256:c57c48337ec7e21be65c56656d26cef4bba5b4149b0027252d832b2965d079db                                                                                                        0.0s
 => => exporting config sha256:69510b4cb905be7494e9946d7d46e922f4b4d9aeb2add488b9f558ac102afbe3                                                                                                          0.0s
 => => exporting attestation manifest sha256:3111876895b3d219781217aa4f26b2456994199324e8d8b2cb10a9bc248783b4                                                                                            0.0s
 => => exporting manifest list sha256:7afb05ae971e964430750af57a699667ecaf5b2399de2be3a48656789ded5a93                                                                                                   0.0s
 => => naming to docker.io/library/assignment1-app:latest                                                                                                                                                0.0s
 => => unpacking to docker.io/library/assignment1-app:latest                                                                                                                                             0.0s
 => resolving provenance for metadata file                                                                                                                                                               0.0s
[+] Building 1/1
 ✔ assignment1-app  Built                                                                                                                                                                                0.0s 
root@DESKTOP-B65U02L:/home/user/cloudComputing/Assignment1# docker compose up
[+] Running 1/1
 ✔ Container assignment1-app-1  Recreated                                                                                                                                                                0.2s 
Attaching to app-1, db-1
db-1  | 
db-1  | PostgreSQL Database directory appears to contain a database; Skipping initialization
db-1  | 
db-1  | 2025-09-10 01:00:19.505 UTC [1] LOG:  starting PostgreSQL 16.10 (Debian 16.10-1.pgdg13+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 14.2.0-19) 14.2.0, 64-bit
db-1  | 2025-09-10 01:00:19.506 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db-1  | 2025-09-10 01:00:19.506 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db-1  | 2025-09-10 01:00:19.513 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db-1  | 2025-09-10 01:00:19.523 UTC [29] LOG:  database system was shut down at 2025-09-10 00:58:22 UTC
db-1  | 2025-09-10 01:00:19.539 UTC [1] LOG:  database system is ready to accept connections
app-1  | === Summary ===
app-1  | {
app-1  |   "total_trips": 6,
app-1  |   "avg_fare_by_city": [
app-1  |     {
app-1  |       "city": "New York",
app-1  |       "avg_fare": 19.0
app-1  |     },
app-1  |     {
app-1  |       "city": "San Francisco",
app-1  |       "avg_fare": 20.25
app-1  |     },
app-1  |     {
app-1  |       "city": "Charlotte",
app-1  |       "avg_fare": 16.25
app-1  |     }
app-1  |   ],
app-1  |   "top_by_fare": [
app-1  |     {
app-1  |       "city": "San Francisco",
app-1  |       "duration": 28,
app-1  |       "fare": 29.3
app-1  |     },
app-1  |     {
app-1  |       "city": "New York",
app-1  |       "duration": 26,
app-1  |       "fare": 27.1
app-1  |     },
app-1  |     {
app-1  |       "city": "Charlotte",
app-1  |       "duration": 21,
app-1  |       "fare": 20.0
app-1  |     }
app-1  |   ]
app-1  | }
app-1 exited with code 0
```
## Outputs
Outputs are written to the "./out/summary.json" file

## Help

1. Wrong db username, password from the environment variables provided in the app section of the docker compose will cause authentication errors.
2. For unique queries they must be formatted to json standards to be included in the summary.json or otherwise the application will crash.

