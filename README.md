german-pos-dict
===============

A German part-of-speech dictionary that can be used from Java. This repo contains no code
but [Morfologik](https://github.com/morfologik/) binary files to look up part-of-speech data.
As a developer, consider using [LanguageTool](https://github.com/languagetool-org) instead
of this. If you really want to use this directly, please check out the unit tests for examples.

Also use LanguageTool to export the data in these dictionaries, [as documented here](http://wiki.languagetool.org/developing-a-tagger-dictionary#toc2).

The POS tags are documented [here](https://morphy.wolfganglezius.de/content/2-download/wklassen.pdf).

## Internal

To prepare a release (note this will only *add* forms, not remove them):

* call `./download-data.sh`
* set `DBUSER`, `DBPASS`, and `LT_PASS` in `./data-to-dict.sh`
* call `./data-to-dict.sh`
* increase version in `pom.xml`
* call `mvn install`
* test it from the software that integrates it (including a regression test)

To make a release:

* set the version in `pom.xml` to not include `SNAPSHOT`
* `rm src/main/resources/org/languagetool/resource/de/SynthDictionaryBuilder*tags.txt`
* `mvn clean test`
* `mvn clean deploy -P release`
* go to https://oss.sonatype.org/#stagingRepositories
* scroll to the bottom, select latest version, and click `Release`
* `git tag vx.y`
* `git push origin vx.y`
