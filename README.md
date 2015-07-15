This project demonstrates a discrepancy between Activator and SBT

```sh-session
$ rm -rf ~/.ivy2/cache/com.typesafe.sbtrc/
$ sbt update
...
[warn] 	module not found: com.typesafe.sbtrc#actor-client-2-11;0.3.1
[warn] ==== local: tried
[warn]   /Users/jkutner/.ivy2/local/com.typesafe.sbtrc/actor-client-2-11/0.3.1/ivys/ivy.xml
[warn] ==== public: tried
[warn]   https://repo1.maven.org/maven2/com/typesafe/sbtrc/actor-client-2-11/0.3.1/actor-client-2-11-0.3.1.pom
[info] Resolving jline#jline;2.12.1 ...
[warn] 	::::::::::::::::::::::::::::::::::::::::::::::
[warn] 	::          UNRESOLVED DEPENDENCIES         ::
[warn] 	::::::::::::::::::::::::::::::::::::::::::::::
[warn] 	:: com.typesafe.sbtrc#actor-client-2-11;0.3.1: not found
[warn] 	::::::::::::::::::::::::::::::::::::::::::::::
[warn] 
[warn] 	Note: Unresolved dependencies path:
[warn] 		com.typesafe.sbtrc:actor-client-2-11:0.3.1 (/Users/jkutner/workspace/heroku/kissaten/activator-bug/build.sbt#L7-10)
[warn] 		  +- default:activator-bug_2.11:1.0
...
[error] (*:update) sbt.ResolveException: unresolved dependency: com.typesafe.sbtrc#actor-client-2-11;0.3.1: not found
[error] Total time: 1 s, completed Jul 15, 2015 9:52:31 AM
```

But with Activator, you get this:

```sh-session
$ activator update
...
[info] downloading https://repo.typesafe.com/typesafe/ivy-releases/com.typesafe.sbtrc/actor-client-2-11/0.3.1/jars/actor-client-2-11.jar ...
[info] 	[SUCCESSFUL ] com.typesafe.sbtrc#actor-client-2-11;0.3.1!actor-client-2-11.jar (1613ms)
...
[info] Done updating.
[success] Total time: 47 s, completed Jul 15, 2015 9:51:56 AM
```

With sbt, if you add this resolver, it will work:

```
resolvers += Resolver.url("Typesafe Ivy releases", url("https://repo.typesafe.com/typesafe/ivy-releases"))(Resolver.ivyStylePatterns)
```

Related issues:
https://github.com/playframework/playframework/issues/4839
https://github.com/typesafehub/activator/issues/979
https://github.com/sbt/sbt/issues/2054
