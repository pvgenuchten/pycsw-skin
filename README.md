# pycsw-skin

A customisation of the standard [pycsw](https://github.com/geopython/pycsw) templates

## Installation

Copy the contents of this repo into /pycsw/ogc/api/templates.

## K8s

Add the files in a k8s configmap, then manage individual file overrides using subpath:

```
kubectl create configmap cm_pycsw --from-file=./ --dry-run=client -o yaml > cm_pycsw.yml
```

## Docker

Override relevant template files:

```
docker run -p8000:8000 
  -v${PWD}/_base.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/_base.html 
  -v${PWD}/collection.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/collection.html 
  -v${PWD}/items.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/items.html 
  -v${PWD}/item.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/item.html 
  -v${PWD}/collections.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/collections.html 
  -v${PWD}/search_and_recent.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/search_and_recent.html 
  -v${PWD}/landing_page.html:/home/pycsw/pycsw/pycsw/ogc/api/templates/landing_page.html 
  geopython/pycsw
```

## Load records

Load a set of records using pycsw-admin
```
python3 pycsw-admin.py load-records --config default.cfg --path /path/to/records
```
(-r recurses through child folders)