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
load("@graknlabs_build_tools//checkstyle:rules.bzl", "checkstyle_test")

java_test(
    name = "conjunction-query-test",
    test_class = "grakn.core.graql.gremlin.ConjunctionQueryTest",
    srcs = ["ConjunctionQueryTest.java", "GraqlMatchers.java"],
    deps = [
        "//concept:concept",
        "//server:server",

        "@graknlabs_graql//java:graql",

        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//dependencies/maven/artifacts/org/mockito:mockito-core",
    ],
    size = "small"
)

java_test(
    name = "graql-traversal-test",
    test_class = "grakn.core.graql.gremlin.GraqlTraversalTest",
    srcs = ["GraqlTraversalIT.java", "GraqlMatchers.java"],
    deps = [
        "//common:common",
        "//concept:concept",
        "//server:server",
        "//test-integration/graql/graph:movie-graph",
        "//test-integration/rule:grakn-test-server",

        "@graknlabs_graql//java:graql",

        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//dependencies/maven/artifacts/com/google/guava:guava",
        "//dependencies/maven/artifacts/org/mockito:mockito-core",
    ],
    size = "small"
)

checkstyle_test(
    name = "checkstyle",
    targets = [
        ":graql-traversal-test",
        ":conjunction-query-test"
    ],
)