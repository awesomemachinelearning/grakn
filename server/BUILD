#
# GRAKN.AI - THE KNOWLEDGE GRAPH
# Copyright (C) 2019 Grakn Labs Ltd
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.
#

package(default_visibility = ["//visibility:public"])

load("@graknlabs_build_tools//distribution/maven:rules.bzl", "assemble_maven", "deploy_maven")
load("@graknlabs_bazel_distribution//apt:rules.bzl", "assemble_apt", "deploy_apt")
load("@graknlabs_bazel_distribution//common:rules.bzl", "assemble_targz", "java_deps", "assemble_zip")
load("@graknlabs_bazel_distribution//rpm:rules.bzl", "assemble_rpm", "deploy_rpm")
load("@graknlabs_build_tools//checkstyle:rules.bzl", "checkstyle_test")

exports_files(
    glob(["conf/**", "services/**"]),
    visibility = ["//visibility:public"]
)


genrule(
    name = "version",
    srcs = [
        "src/server/templates/Version.java",
        "//:VERSION",
    ],
    cmd = "VERSION=`cat $(location //:VERSION)`;sed -e \"s/{version}/$$VERSION/g\" $(location src/server/templates/Version.java) >> $@",
    outs = ["Version.java"],
    visibility = ["//common:__subpackages__"],
)

java_library(
    name = "server",
    srcs = glob(["src/**/*.java"], exclude=["**/templates/**", "**/test/**"]) + [":version"],
    deps = [
        # Internal dependencies
        "//api:api",
        "//common:common",
        "//concept:concept",

        # External dependencies from @graknlabs
        "@graknlabs_graql//java:graql",
        "@graknlabs_protocol//grpc/java:protocol",
        "@graknlabs_benchmark//lib:server-instrumentation",

        # External dependencies from Maven
        "//dependencies/maven/artifacts/com/datastax/cassandra:cassandra-driver-core",
        "//dependencies/maven/artifacts/org/apache/cassandra:cassandra-thrift",
        "//dependencies/maven/artifacts/org/apache/hadoop:hadoop-annotations",
        "//dependencies/maven/artifacts/com/google/auto/value:auto-value",
        "//dependencies/maven/artifacts/com/google/code/findbugs:jsr305",
        "//dependencies/maven/artifacts/com/google/guava:guava",
        "//dependencies/maven/artifacts/commons-cli:commons-cli", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/commons-configuration:commons-configuration", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/commons-lang:commons-lang",
        "//dependencies/maven/artifacts/io/grpc:grpc-core",
        "//dependencies/maven/artifacts/io/grpc:grpc-stub",
        "//dependencies/maven/artifacts/io/zipkin/brave:brave",
        "//dependencies/maven/artifacts/org/apache/cassandra:cassandra-all", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/thrift:libthrift",
        "//dependencies/maven/artifacts/org/apache/commons:commons-lang3", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/hadoop:hadoop-common", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/hadoop:hadoop-mapreduce-client-core", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/spark:spark-core-2-11",
        "//dependencies/maven/artifacts/org/apache/spark:spark-launcher-2-11", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/tinkerpop:gremlin-core", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/apache/tinkerpop:hadoop-gremlin",
        "//dependencies/maven/artifacts/org/apache/tinkerpop:spark-gremlin",
        "//dependencies/maven/artifacts/org/apache/tinkerpop:tinkergraph-gremlin",
        "//dependencies/maven/artifacts/org/janusgraph:janusgraph-cassandra",
        "//dependencies/maven/artifacts/org/janusgraph:janusgraph-core",
        "//dependencies/maven/artifacts/org/janusgraph:janusgraph-hadoop",
        "//dependencies/maven/artifacts/org/scala-lang:scala-library", # PREVIOUSLY UNDECLARED
        "//dependencies/maven/artifacts/org/slf4j:slf4j-api"
    ],
    runtime_deps = [
        "//dependencies/maven/artifacts/ch/qos/logback:logback-classic",
        "//dependencies/maven/artifacts/ch/qos/logback:logback-core",
        "//dependencies/maven/artifacts/io/grpc:grpc-netty",
        "//dependencies/maven/artifacts/javax/servlet:javax-servlet-api", # PREVIOUSLY UNDECLARED
    ],
    resources = ["LICENSE"] + glob(["resources/*"]),
    resource_strip_prefix = "server",
    tags = ["maven_coordinates=io.grakn.core:grakn-server:{pom_version}"],
    visibility = ["//visibility:public"]

)

checkstyle_test(
    name = "checkstyle",
    targets = [
        ":server"
    ],
)

java_binary(
    name = "server-binary",
    main_class = "grakn.core.daemon.GraknDaemon",
    runtime_deps = [
        "//daemon",
        "//server"
    ],
    visibility = ["//:__pkg__"],
)

java_deps(
    name = "server-deps",
    target = ":server-binary",
    java_deps_root = "server/services/lib/",
    version_file = "//:VERSION",
    visibility = ["//:__pkg__"]
)

assemble_targz(
    name = "assemble-linux-targz",
    output_filename = "grakn-core-server-linux",
    targets = [":server-deps", "//bin:assemble-bash-targz"],
    additional_files = {
        "//server:conf/logback.xml": "server/conf/logback.xml",
        "//server:conf/grakn.properties": "server/conf/grakn.properties",
        "//server:services/cassandra/cassandra.yaml": "server/services/cassandra/cassandra.yaml",
        "//server:services/cassandra/logback.xml": "server/services/cassandra/logback.xml",
        "//server:services/grakn/grakn-core-ascii.txt": "server/services/grakn/grakn-core-ascii.txt"
    },
    empty_directories = [
        "server/db/cassandra",
        "server/db/queue"
    ],
    permissions = {
      "server/services/cassandra/cassandra.yaml": "0777",
      "server/db/cassandra": "0777",
      "server/db/queue": "0777",
    },
    visibility = ["//visibility:public"]
)

assemble_zip(
    name = "assemble-mac-zip",
    output_filename = "grakn-core-server-mac",
    targets = [":server-deps", "//bin:assemble-bash-targz"],
    additional_files = {
        "//server:conf/logback.xml": "server/conf/logback.xml",
        "//server:conf/grakn.properties": "server/conf/grakn.properties",
        "//server:services/cassandra/cassandra.yaml": "server/services/cassandra/cassandra.yaml",
        "//server:services/cassandra/logback.xml": "server/services/cassandra/logback.xml",
        "//server:services/grakn/grakn-core-ascii.txt": "server/services/grakn/grakn-core-ascii.txt"
    },
    empty_directories = [
        "server/db/cassandra",
        "server/db/queue"
    ],
    permissions = {
      "server/services/cassandra/cassandra.yaml": "0777",
      "server/db/cassandra": "0777",
      "server/db/queue": "0777",
    },
    visibility = ["//visibility:public"]
)

assemble_zip(
    name = "assemble-windows-zip",
    output_filename = "grakn-core-server-windows",
    targets = [":server-deps", "//bin:assemble-bat-targz"],
    additional_files = {
        "//server:conf/logback.xml": "server/conf/logback.xml",
        "//server:conf/grakn.properties": "server/conf/grakn.properties",
        "//server:services/cassandra/cassandra.yaml": "server/services/cassandra/cassandra.yaml",
        "//server:services/cassandra/logback.xml": "server/services/cassandra/logback.xml",
        "//server:services/grakn/grakn-core-ascii.txt": "server/services/grakn/grakn-core-ascii.txt",
        "//server:services/hadoop/bin/winutils.exe": "server/services/hadoop/bin/winutils.exe"
    },
    empty_directories = [
        "server/db/cassandra",
        "server/db/queue"
    ],
    permissions = {
      "server/services/cassandra/cassandra.yaml": "0777",
      "server/db/cassandra": "0777",
      "server/db/queue": "0777",
    },
    visibility = ["//visibility:public"]
)

assemble_maven(
    name = "assemble-maven",
    target = ":server",
    package = "server",
    version_file = "//:VERSION",
    workspace_refs = "@graknlabs_grakn_core_workspace_refs//:refs.json"
)

deploy_maven(
    name = "deploy-maven",
    target = ":assemble-maven"
)

assemble_apt(
    name = "assemble-linux-apt",
    package_name = "grakn-core-server",
    maintainer = "Grakn Labs <community@grakn.ai>",
    description = "Grakn Core (server)",
    version_file = "//:VERSION",
    depends = [
      "openjdk-8-jre",
      "grakn-core-bin (={version})"
    ],
    archives = [":server-deps"],
    installation_dir = "/opt/grakn/core/",
    files = {
        "//server:conf/logback.xml": "server/conf/logback.xml",
        "//server:conf/grakn.properties": "server/conf/grakn.properties",
        "//server:services/cassandra/cassandra.yaml": "server/services/cassandra/cassandra.yaml",
        "//server:services/cassandra/logback.xml": "server/services/cassandra/logback.xml",
        "//server:services/grakn/grakn-core-ascii.txt": "server/services/grakn/grakn-core-ascii.txt"
    },
    empty_dirs = [
        "opt/grakn/core/server/services/lib/",
        "var/lib/grakn/db/queue",
        "var/lib/grakn/db/cassandra"
     ],
    permissions = {
        "var/lib/grakn/db/queue": "0777",
        "var/lib/grakn/db/cassandra": "0777",
    },
    symlinks = {
        "opt/grakn/core/server/db/": "/var/lib/grakn/db/",
    },
)

deploy_apt(
    name = "deploy-apt",
    target = ":assemble-linux-apt",
    deployment_properties = "@graknlabs_build_tools//:deployment.properties",
)

assemble_rpm(
    name = "assemble-linux-rpm",
    package_name = "grakn-core-server",
    installation_dir = "/opt/grakn/core/",
    version_file = "//:VERSION",
    spec_file = "//config/rpm:grakn-core-server.spec",
    archives = [":server-deps"],
    empty_dirs = [
        "opt/grakn/core/server/services/lib/",
        "var/lib/grakn/db/queue",
        "var/lib/grakn/db/cassandra"
     ],
    files = {
        "//server:conf/logback.xml": "server/conf/logback.xml",
        "//server:conf/grakn.properties": "server/conf/grakn.properties",
        "//server:services/cassandra/cassandra.yaml": "server/services/cassandra/cassandra.yaml",
        "//server:services/cassandra/logback.xml": "server/services/cassandra/logback.xml",
        "//server:services/grakn/grakn-core-ascii.txt": "server/services/grakn/grakn-core-ascii.txt"
    },
    permissions = {
        "services/cassandra/cassandra.yaml": "0777",
        "var/lib/grakn/db/queue": "0777",
        "var/lib/grakn/db/cassandra": "0777",
    },
    symlinks = {
        "opt/grakn/core/server/db/": "/var/lib/grakn/db/",
    },
)

deploy_rpm(
    name = "deploy-rpm",
    target = ":assemble-linux-rpm",
    deployment_properties = "@graknlabs_build_tools//:deployment.properties",
)
