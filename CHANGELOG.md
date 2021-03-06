Changes for 2.2.6
=================
- Fixed the issue with the ```coberturaCheck``` task that was causing it to 
  skip instrumentation (Issue #63)
  
- Fixed dry-run behavior (Issue #64)

Changes for 2.2.5
=================
- Added support for Cobertura's ```encoding``` option when generating reports
  (Issue #43)

- Added the cobertura version to the up-to-date checks so that we re-instrument
  if the version changes (Issue #52)

- Fixed the way the plugin tells Cobertura where source directories are.  The
  coverageSourceDirs argument always allowed users to configure this setting, 
  but the default (srcSets.main.java.srcDirs) was set at apply time, so any
  changes made to source sets in build.gradle was being ignored.  The default
  is now handled at execution time (Issue #53)

- The plugin is now available on the Gradle Plugin Portal (Issue #54)

- The plugin can now be applied by 2 names, 'cobertura', and
  'net.saliman.cobertura' (Issue #59)


Changes for 2.2.4
=================
- Added support for customizing the auxiliary classpath, with thanks to Harald
  Schmitt (Issue #24)

Changes for 2.2.3
=================
- Added support for the Gradle dashboard, with thanks to vyazelenko (Issues #45
  and #46)

Changes for 2.2.2
=================
- Fixed the Auxiliary classpath on Windows boxes. (Issue #39)

- Fixed (again) the classpath issue that was leading to ASM conflicts.  The
  plugin now uses its own child-first classloader to make sure we get the
  versions Cobertura needs ahead of the classes used by the application.

Changes for 2.2.1
=================
- Fixed the operation of the coverageClassesTask and coverageTestTask closures.
  (Issue #38)

Changes for 2.2.0
=================
- One of the biggest changes in this release is the behavior of the "cobertura"
  task.  In 2.1.0, it was made to run all the tests in the applying project, as
  well as tests named "test" in other parts of a multi-project build.  This
  produced undesirable coupling between projects, so this has been removed in
  2.2.0.  The "cobertura" task now runs only the tests in project. (issue #31)

- The exact tasks that get run by the "cobertura" task can be configured by
  setting the coverageTestTasks closure.  Ths no-arg closure returns the
  collection of tasks that should run before the coverage report is generated.

- Users who need to use older versions of Cobertura can now do so without the
  Cobertura libraries getting in the way. Some options, such as
  coverageIgnoreTrivial only work in Cobertura 2.0, so attempting to set those
  properties in the cobertura block of your build.gradle will result in an
  error.

- Groovy and Scala plugins may now be applied before or after the cobertura
  plugin. (issue #35 and issue #37)

- If the coberturaReport is in the task graph, the up-to-date status of all
  tests is set to false (issue #33)

- A Cobertura Check task has been implemented (issue #29) to check test coverage
  levels.

- Support for merging datafiles before generating reports (Issue #10).  This has
  the most value in the parent project of a multi project build.  When this
  happens, the parent project will need to declare a test task dependency on
  all the child project testing tasks to make sure the reports are accurate.

- I've added more tests, and hope to add even more soon.

Changes for 2.1.0
=================
- Added the coberturaReport task to generate coverage reports. (issue #20)

- The cobertura task now depends on tasks of type test in the applying project,
  and tasks named test in child projects (but not all tasks of type test in the
  child project).  It no longer runs tests in parent projects, sibling projects
  or tests in child projects that are not named "test". (issue #14)

- The coverageSourceDirs extension property now looks for scala and groovy code
  by default. (issues #7 and #22)

- Instrumentation now happens only when source code has changed or the cobertura
  configuration has changed. (issue #23)

- Instrumentation now depends on the classes task so that changes to Groovy
  or Scala source code triggers re-instrumentation. (issue #15)

- The plugin adjusts dependencies for test tasks added after the plugin is
  applied (issue #21)

Changes for 2.0.0
=================
- Updated the plugin to work with Gradle 1.7.  Dropped support for prior
  versions of Gradle.

Changes for 1.2.0
=================
- Added support for Cobertura 2.0 and its extra configuration options.

- Fixed bug that caused the configuration of test tasks to fail on sub-projects
  that don't have the coberura plugin applied. (issue #8)
