# Gradle Multimodule 구조에서 일부 모듈을 maven repository에 publish하는 방법

```kotlin
tasks.withType<Jar> {
    from(project(":subModuleA").sourceSets["main"].output)
    from(project(":subModuleB").sourceSets["main"].output)
    from(project(":subModuleC").sourceSets["main"].output)
}

publishing {
    ...
    publications {
        create<MavenPublication>("maven") {
            configurations["runtimeElements"].hierarchy.forEach {
                it.dependencies.removeIf { dependency -> dependency.group == "GROUP_TO_EXCLUDE" }
            }
            from(components["java"])
            artifactId = "my-artifact"

            pom {
                withXml {
                    val dependenciesNode = ((asNode().get("dependencies") as NodeList).firstOrNull() as Node?)
                    dependenciesNode?.let {
                        it.children().removeIf { dependencyNode ->
                            (dependencyNode as Node).children().any { node ->
                                val nodeName = ((node as Node).name() as QName).localPart
                                nodeName == "groupId" && node.text() == "GROUP_TO_EXCLUDE"
                            }
                        }
                    }
                }
            }
        }
    }
    ...
}
```


## Reference
- https://stackoverflow.com/questions/53353379/publishing-artifact-directly-including-gradle-submodules
- https://stackoverflow.com/questions/68470193/exclude-dependency-from-pom-using-maven-publish-plugin
