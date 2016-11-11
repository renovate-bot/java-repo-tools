# Releasing

In general, follow the [instructions at Sonatype for using the Maven release
plugin](http://central.sonatype.org/pages/apache-maven.html).

## Release the checkstyle-config package

First, release the checkstyle-config package.

    cd checkstyle-config
    mvn release:clean release:prepare

This creates commits for the release and tags it. Next, update the parent pom
to use the latest snapshot version so that the tests continue to pass.

    # Update the version in the checkstyle plugin resource dependencies.
    vim ../pom.xml
    git add ../pom.xml
    git commit
    git push origin branchname

Then, make a pull request for the release. After verifying that it works,
perform the release to upload it to Maven Central.

    mvn release:perform

## Release the shared-configuration package

After releasing the checkstyle-config package, update the root `pom.xml` to
depend on the released version.

    # Use the latest released version of checkstyle-config.
    vim pom.xml
    git add pom.xml
    git commit

Next, prepare a release.

    mvn release:clean release:prepare

Next, update the version of the parent in `test/pom.xml`. Also update `pom.xml`
to use the latest snapshot of checkstyle-config.

Then, make a pull request for the release. After verifying that it works,
perform the release to upload it to Maven Central.

    mvn release:perform

