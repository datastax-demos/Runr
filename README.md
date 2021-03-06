# Runr Demo

Load the schema
```
cd ../cql
cqlsh -f runr.cql
```

Load the Solr cores
```
cd ../solr
dsetool create_core runr.runner_tracking schema=runr_runner_tracking_schema.xml solrconfig=runr_runner_tracking_config.xml
dsetool create_core runr.runners schema=runr_runners_schema.xml solrconfig=runr_runners_config.xml
```

Install Python Dependencies
```
pip install numpy
pip install LatLon
pip install orderedset
```

Load the data
```
cd ../data-loader
python load_positions.py
python load_runners.py
```

Run the Web Interface
```
cd ../web
./run
```

Build and submit the spark job
```
cd ../calculate-position
sbt package
dse spark-submit --class position_calculator target/scala-2.10/calculate-position_2.10-1.0.jar
```
