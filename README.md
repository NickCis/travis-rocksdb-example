[![Build Status](https://travis-ci.org/NickCis/travis-rocksdb-example.svg)](https://travis-ci.org/NickCis/travis-rocksdb-example)

# Ejemplo para usar rocksdb en travis-ci

Este es un ejemplo muy simple de instalar las dependencias necesarias para que en [travis](travis-ci.org) se pueda usar rocksdb.

## Explicaci&oacute;n

Para disminuir los tiempos de build, se evita compilando rocksdb. Se baja el paquete generado en [este repositorio](https://github.com/NickCis/rocksdb). Dicho paquete es creado por travis del repositorio. Ver [Nickcis/rocksdb/.travis.yml](https://github.com/NickCis/rocksdb/blob/master/.travis.yml) para entender como se genero.

Para configurar el entorno, basicamente lo que se esta haciendo es generar una carpeta, `root`, que se usa como base para instalar de forma local todos los paquetes que travis, por politicas de seguridad, no nos deja instalar.

Despues de haber bajado los paquetes y extraidos, tendremos la siguiente estructura de carpetas:
```
.
├── CMakeLists.txt
├── libgflags0_2.0-1_amd64.deb
├── libgflags-dev_2.0-1_amd64.deb
├── README.md
├── rocksdb_3.10-0.deb
├── root
│   ├── bin
│   └── usr
│       ├── bin
│       │   ├── g++ -> /usr/bin/g++-5
│       │   ├── gcc -> /usr/bin/gcc-5
│       │   └── gflags_completions.sh
│       ├── include
│       │   ├── gflags
│       │   │   ├── gflags_completions.h
│       │   │   ├── gflags_declare.h
│       │   │   └── gflags.h
│       │   ├── google
│       │   │   ├── gflags_completions.h
│       │   │   └── gflags.h
│       │   └── rocksdb
│       │       ├── cache.h
│       │       ├── c.h
│       │       ├── compaction_filter.h
│       │       ├── comparator.h
│       │       ├── db.h
│       │       ├── env.h
│       │       ├── experimental.h
│       │       ├── filter_policy.h
│       │       ├── flush_block_policy.h
│       │       ├── immutable_options.h
│       │       ├── iostats_context.h
│       │       ├── iterator.h
│       │       ├── ldb_tool.h
│       │       ├── listener.h
│       │       ├── memtablerep.h
│       │       ├── merge_operator.h
│       │       ├── metadata.h
│       │       ├── options.h
│       │       ├── perf_context.h
│       │       ├── rate_limiter.h
│       │       ├── slice.h
│       │       ├── slice_transform.h
│       │       ├── sst_dump_tool.h
│       │       ├── statistics.h
│       │       ├── status.h
│       │       ├── table.h
│       │       ├── table_properties.h
│       │       ├── thread_status.h
│       │       ├── transaction_log.h
│       │       ├── types.h
│       │       ├── universal_compaction.h
│       │       ├── utilities
│       │       │   ├── backupable_db.h
│       │       │   ├── checkpoint.h
│       │       │   ├── convenience.h
│       │       │   ├── db_ttl.h
│       │       │   ├── document_db.h
│       │       │   ├── flashcache.h
│       │       │   ├── geo_db.h
│       │       │   ├── json_document.h
│       │       │   ├── leveldb_options.h
│       │       │   ├── spatial_db.h
│       │       │   ├── stackable_db.h
│       │       │   ├── utility_db.h
│       │       │   └── write_batch_with_index.h
│       │       ├── version.h
│       │       ├── write_batch_base.h
│       │       └── write_batch.h
│       ├── lib
│       │   ├── libgflags.a
│       │   ├── libgflags.la
│       │   ├── libgflags_nothreads.a
│       │   ├── libgflags_nothreads.la
│       │   ├── libgflags_nothreads.so -> libgflags_nothreads.so.2.1.0
│       │   ├── libgflags_nothreads.so.2 -> libgflags_nothreads.so.2.1.0
│       │   ├── libgflags_nothreads.so.2.1.0
│       │   ├── libgflags.so -> libgflags.so.2.1.0
│       │   ├── libgflags.so.2 -> libgflags.so.2.1.0
│       │   ├── libgflags.so.2.1.0
│       │   ├── librocksdb.a
│       │   ├── librocksdb.so
│       │   ├── librocksdb.so.3
│       │   ├── librocksdb.so.3.10
│       │   ├── librocksdb.so.3.10.0
│       │   └── pkgconfig
│       │       ├── libgflags_nothreads.pc
│       │       └── libgflags.pc
│       └── share
│           └── doc
│               ├── libgflags0
│               │   ├── changelog.Debian.gz
│               │   ├── changelog.gz
│               │   └── copyright
│               └── libgflags-dev
│                   ├── AUTHORS
│                   ├── changelog.Debian.gz
│                   ├── changelog.gz
│                   ├── ChangeLog.gz
│                   ├── COPYING
│                   ├── copyright
│                   ├── designstyle.css
│                   ├── gflags.html
│                   ├── INSTALL.gz
│                   ├── NEWS.gz
│                   └── README
└── src
    └── simple_example.cpp
```

Se setean las variables de entorno `PATH`, `LIBRARY_PATH`, `LD_LIBRARY_PATH`, `CPATH`, `GXX` y `CC` para que las librerias y binarios instalados en la carpeta  `./root/` tengan una mayor prioridad que lo instalado en las carpetas del sistema base.
