# Tipo de cambio documentation!

## Description

Este proyecto busca calcular el tipo de cambio de acuerdo a la cantidad de préstamos hipotecarios y/o prendarios, o predecir la cantidad de préstamos hipotecarios de acuerdo al tipo de cambio.

## Commands

The Makefile contains the central entry points for common tasks related to this project.

### Syncing data to cloud storage

* `make sync_data_up` will use `aws s3 sync` to recursively sync files in `data/` up to `s3://s3://mi-bucket-aws/data/`.
* `make sync_data_down` will use `aws s3 sync` to recursively sync files from `s3://s3://mi-bucket-aws/data/` to `data/`.


