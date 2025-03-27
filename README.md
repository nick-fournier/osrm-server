# osrm-server
My locally hosted OSRM server bundle for walk, bike, drive


# Steps to process OSM data

1. Download OSM data
```bash
wget https://download.geofabrik.de/europe/germany/us-west-latest.osm.pbf
```

2. Run the docker container to extract the data
```bash
docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-extract -p /opt/car.lua /data/us-west-latest.osm.pbf || echo "osrm-extract failed"
```

To run with a custom profile, you can use the following command:
```bash
docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-extract -p /data/bicycle_wrongways.lua /data/us-west-latest.osm.pbf || echo "osrm-extract failed"
```

3. Run the docker container to prepare the data
```bash
docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-partition /data/us-west-latest.osrm || echo "osrm-partition failed"
```

4. Run the docker container to customize the data
```bash
docker run -t -v "${PWD}:/data" ghcr.io/project-osrm/osrm-backend osrm-customize /data/us-west-latest.osrm || echo "osrm-customize failed"
```

