load("@graknlabs_build_tools//checkstyle:rules.bzl", "checkstyle_test")

java_test(
    name = "query-equivalence-it",
    size = "medium",
    srcs = ["AtomicQueryEquivalenceIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = ["//test-integration/graql/reasoner/resources:generic-schema"],
    test_class = "grakn.core.graql.reasoner.query.AtomicQueryEquivalenceIT",
    deps = [
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "atomic-query-it",
    size = "medium",
    srcs = ["AtomicQueryIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = ["//test-integration/graql/reasoner/resources:generic-schema"],
    test_class = "grakn.core.graql.reasoner.query.AtomicQueryIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "explanation-it",
    size = "medium",
    srcs = [
        "ExplanationIT.java",
    ],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/stubs:reasoning-stubs",
    ],
    test_class = "grakn.core.graql.reasoner.query.ExplanationIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/commons-collections",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/graql/reasoner/graph:geo-graph",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "materialisation-it",
    size = "medium",
    srcs = ["MaterialisationIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = ["//test-integration/graql/reasoner/resources:materialisation"],
    test_class = "grakn.core.graql.reasoner.query.MaterialisationIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/graql/reasoner/graph:geo-graph",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "negation-it",
    size = "medium",
    srcs = [
        "NegationIT.java",
    ],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/resources/recursion:recursion-schemas",
        "//test-integration/graql/reasoner/stubs:reasoning-stubs",
    ],
    test_class = "grakn.core.graql.reasoner.query.NegationIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/commons-collections",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/graql/reasoner/graph:reachability-graph",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "query-unification-it",
    size = "medium",
    srcs = [
        "AtomicQueryUnificationIT.java",
    ],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/resources:generic-schema",
        "//test-integration/graql/reasoner/resources:unification-with-types",
    ],
    test_class = "grakn.core.graql.reasoner.query.AtomicQueryUnificationIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/commons-collections",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/graql/reasoner/graph:generic-schema-graph",
        "//test-integration/graql/reasoner/graph:geo-graph",
        "//test-integration/graql/reasoner/pattern:query-pattern",
        "//test-integration/graql/reasoner/pattern:relation-pattern",
        "//test-integration/graql/reasoner/pattern:resource-pattern",
        "//test-integration/graql/reasoner/pattern:type-pattern",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "query-it",
    size = "medium",
    srcs = ["QueryIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    test_class = "grakn.core.graql.reasoner.query.QueryIT",
    deps = [
        "//concept",
        "//server",
        "//test-integration/graql/reasoner/graph:geo-graph",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@com-google-guava-guava//jar",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "ontological-query-it",
    size = "large",
    srcs = ["OntologicalQueryIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/resources:matching-types",
        "//test-integration/graql/reasoner/resources:rule-applicability",
    ],
    test_class = "grakn.core.graql.reasoner.query.OntologicalQueryIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "resolution-plan-it",
    size = "medium",
    srcs = ["ResolutionPlanIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = ["//test-integration/graql/reasoner/resources:resolution-plan"],
    test_class = "grakn.core.graql.reasoner.query.ResolutionPlanIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "semantic-difference-it",
    size = "medium",
    srcs = ["SemanticDifferenceIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/resources:generic-schema",
    ],
    test_class = "grakn.core.graql.reasoner.query.SemanticDifferenceIT",
    deps = [
        "//concept",
        "//dependencies/maven/artifacts/com/google/guava",
        "//server",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

java_test(
    name = "subsumption-it",
    size = "medium",
    srcs = ["SubsumptionIT.java"],
    classpath_resources = ["//test-integration/resources:logback-test"],
    resources = [
        "//test-integration/graql/reasoner/resources:generic-schema",
    ],
    test_class = "grakn.core.graql.reasoner.query.SubsumptionIT",
    deps = [
        "//dependencies/maven/artifacts/com/google/guava",
        "//dependencies/maven/artifacts/commons-collections",
        "//dependencies/maven/artifacts/org/hamcrest:hamcrest-library",
        "//server",
        "//test-integration/graql/reasoner/graph:generic-schema-graph",
        "//test-integration/graql/reasoner/pattern:query-pattern",
        "//test-integration/graql/reasoner/pattern:relation-pattern",
        "//test-integration/graql/reasoner/pattern:resource-pattern",
        "//test-integration/graql/reasoner/pattern:type-pattern",
        "//test-integration/rule:grakn-test-server",
        "//test-integration/util:graql-test-util",
        "@graknlabs_graql//java:graql",
    ],
)

checkstyle_test(
    name = "checkstyle",
    targets = [
        ":atomic-query-it",
        ":query-equivalence-it",
        ":explanation-it",
        ":materialisation-it",
        ":negation-it",
        ":query-unification-it",
        ":query-it",
        ":ontological-query-it",
        ":resolution-plan-it",
        ":semantic-difference-it",
        "//test-integration/graql/reasoner/query:subsumption-it",
    ],
)
