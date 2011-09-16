# Sonatype POMs

These are POMs we use to publish libraries to [Maven Central][3] via
[Sonatype][1]'s [third-party publication][2] service.  Libraries:

## Lessen

We are considering the former Metaweb's [Lessen][4] revision 8 to be 1.0.

Checkout Lessen rev8 in the `lessen/` directory:

```
% cd lessen
% svn co -r8 http://lessen.googlecode.com/svn/trunk/ .
% mvn source:jar javadoc:jar package gpg:sign repository:bundle-create
```

(Lessen doesn't have any external dependencies and easily built in Maven).

## Whirlycache

While [Whirlycache][5] has moved to GitHub and continues active development,
the older version [1.0.1][6] is what our source currently depends on.

Checkout Whirlycache 1.0.1 into whirlycache, and install the outdated Hibernate
JAR into your local repository, which does not appear to available in Maven
repositories anywhere:

```
% cd whirlycache
% svn co https://svn.java.net/svn/whirlycache~svn/tags/RELEASE_1_0_1/ .
% mvn install:install-file -Dfile=nodistrib/lib/hibernate.jar -DgroupId=org.hibernate -DartifactId=hibernate -Dversion=2 -Dpackaging=jar
% mvn source:jar javadoc:jar package gpg:sign repository:bundle-create
% rm -rf ~/.m2/repository/org/hibernate/hibernate/2/
```

You could probably remove org/hibernate from your local Maven repository
with no ill effects, other than re-downloading artifacts later if you're
actively developing against them.

[1]: http://nexus.sonatype.org/oss-repository-hosting.html
[2]: https://docs.sonatype.org/display/Repository/Uploading+3rd-party+Artifacts+to+Maven+Central
[3]: http://repo1.maven.org/maven2/
[4]: https://code.google.com/p/lessen/
[5]: https://github.com/whirlycott/Whirlycache
[6]: http://java.net/projects/whirlycache/sources/svn/show/tags/RELEASE_1_0_1?rev=184
