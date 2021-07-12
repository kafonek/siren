### Overview

This repository helps spin up an Elasticsearch-Siren instance and connected Jupyter server. The goal here is to demonstrate some programmatic interaction between Notebooks and Siren, as well as create an easy-to-reproduce-environment for demonstrations or bug reporting.

To get started, clone this repo and run `docker-compose up --build -d && docker-compose logs -f`. It will take a few minutes to build the Docker images, and may take a little longer for the Siren web-server to start even once the image is running.

Look in the Jupyter logs for a link to your server with the access token (something like `http://127.0.0.1:8888/?token=68b704d7cdee14b75051daa4efe55c6d69ee8a306ab29e1f`). The Siren/Kibana UI will be available at `http://localhost:5606`, and ES endpoints at `https://localhost:9220` _(note that Jupyter is running in the same Docker network so you'll see Notebooks connect to `https://siren:9220` vice localhost)_.

### Siren

Siren is an Elasticsearch plugin that adds several features to the base Elasticsearch/Kibana stack, most noteably relationships between tables. See https://siren.io/getting-started/ for more details.

### WSL

If you're using [WSL](https://docs.microsoft.com/en-us/windows/wsl/), you will need to set your docker desktop system `vm.max_map_count` to 262144 or higher. Note this does not persist over system restarts. See https://community.siren.io/t/discovery-type-single-node-not-working-as-expected/390 for discussion at the Siren community. If Siren is not starting, this is probably the reason why. You can sanity check by exec'ing into the Siren container and looking at `/opt/platform/elasticsearch/logs/siren-distribution.log`.

### Relational Datasets

The University of Prague hosts a variety of Relational Dataset Repositories at https://relational.fit.cvut.cz/. If you want to see how Siren works with data besides the demo data, check out `cvut`'s awesome resources. Thanks [CTU](https://www.cvut.cz/en) !!

The Siren container has the mysql-connector jdbc driver installed and copied into the right directory. To add any of the CVUT tables to your Siren instance via Kibana/Siren-Investigate UI, go to Management -> Datasources -> JDBC.

- Database type: Mysql
- Username: `guest`
- Password: `relational`
- Connection string: `jdbc:mysql://relational.fit.cvut.cz:3306?useLegacyDatetimeCode=false&useCursorFetch=true&enabledTLSProtocols=TLSv1.2`

After that, follow the prompts to create a virtual index and index pattern search. Alternatively, pull the data in via Notebooks and write to Elasticsearch programmatically.
