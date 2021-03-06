#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#

set(AVRO_SRC
    avro.h
    avro_private.h
    datafile.c
    datum.c
    datum.h
    datum_equal.c
    datum_read.c
    datum_size.c
    datum_skip.c
    datum_validate.c
    datum_write.c
    dump.c
    dump.h
    encoding.h
    encoding_binary.c
    io.c
    schema.c
    schema.h
    schema_equal.c
    st.c
    st.h
)

set(JANSSON_SRC
    ../jansson/src/dump.c
    ../jansson/src/hashtable.c
    ../jansson/src/hashtable.h
    ../jansson/src/jansson.h
    ../jansson/src/jansson_private.h
    ../jansson/src/load.c
    ../jansson/src/strbuffer.c
    ../jansson/src/strbuffer.h
    ../jansson/src/utf.c
    ../jansson/src/utf.h
    ../jansson/src/util.h
    ../jansson/src/value.c
)

source_group(Avro FILES ${AVRO_SRC})
source_group(Jansson FILES ${JANSSON_SRC})

add_library(avro-static STATIC ${AVRO_SRC} ${JANSSON_SRC})
set_target_properties(avro-static PROPERTIES OUTPUT_NAME avro)
add_library(avro-shared SHARED ${AVRO_SRC} ${JANSSON_SRC})
set_target_properties(avro-shared PROPERTIES
        OUTPUT_NAME avro
        SOVERSION ${AVRO_VERSION})

install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/avro.h DESTINATION include)
install(TARGETS avro-static avro-shared
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
)

