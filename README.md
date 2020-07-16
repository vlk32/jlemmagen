# About this clone

This is clone of [jlemmagen] originaly implemented by [Michal Hlavac][hlavki]

The main goal is publish release version of this library to [mavenCentral()][mavenCentral]

# JLemmagen

JLemmaGen is java implmentation of [LemmaGen][lemmagen] project. It's open source lemmatizer with 15 prebuilted european lexicons.
Of course you can build your own lexicon.

[LemmaGen][lemmagen] project aims at providing standardized open source multilingual platform for lemmatisation.

Project contains 2 libraries:
*    **lemmagen.jar** - implementation of lemmatizer and API for building own lemmatizers
*    **lemmagen-lang.jar** - prebuilted lemmatizers from [Multext Eastern dictionaries][multeast]
    * **IMPORTANT!**  - see [License](#markdown-header-license) chapter.

## Note about lemmatizers
It is possible to use prebuilted from [lexicons] ( see https://github.com/vhyza/lemmagen-lexicons ).
There are free lexicons of 11 languages (bg, cs, en, et, fr, hu, ro, sk, sl-rozaj, sl, uk)
and 5 lexicons for **non commercial usage** ( fa, mk, pl, ru, sr ).
You could build own jar containing only required languages.

### Sample Usage
```java
// find prebuilted lemmatizer via 
// Thread.currentThread().getContextClassLoader().getResourceAsStream("lemmagen/lang/en.lem")
Lemmatizer lm = LemmatizerFactory.getPrebuilt("lemmagen/lang/en");
assert("be".equals(lm.lemmatize("are")));
```

### Maven
```xml
<dependency>
    <groupId>io.github.vlk32</groupId>
    <artifactId>lemmagen</groupId>
    <version>X.Y.Z</version>
</dependency>
```

### Gradle
```groovy
dependencies {
    implementation 'io.github.vlk32:jlemmagen:X.Y.Z'
}
```


### Lucene (Solr)
You need these jars to integrate with lucene/solr:

*    lemmagen-lucene.jar
*    lemmagen.jar
*    lemmagen-lang.jar
*    SLF4J API and implememtation (e.g. slf4j-jdk14.jar)

Example of solr filter definition in schema (e.g. Slovak):
```xml
<filter class="org.apache.lucene.analysis.lemmagen.LemmagenFilterFactory" lexicon="mlteast-sk"/>
<!--
<filter class="org.apache.lucene.analysis.lemmagen.LemmagenFilterFactory" lexicon="lemmagen/lang/sk"/>
-->
```

### Making release

```bash
# commit and tag
git tag X.Y.Z
./gradlew clean build publish 
git push --follow-tags # push tag to repository
```

### License

All source code is licensed under Apache License 2.0.
Important note is that [binary rule tree files][lexicons] (*.lem)
* for languages (bg, cs, en, et, fr, hu, ro, sk, sl-rozaj, sl, uk) are licensed under [Creative Commons - Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)][CCBYSA]
* for languages (fa, mk, pl, ru, sr) are licensed under [Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)][CCBYNC] and **can't be used commercially.**

[jlemmagen]: https://github.com/hlavki/jlemmagen
[lemmagen]: http://lemmatise.ijs.si/Software/Version3
[multeast]: http://nl.ijs.si/ME/V4/
[lexicons]: https://github.com/vhyza/lemmagen-lexicons
[hlavki]: https://github.com/hlavki
[mavenCentral]: https://search.maven.org/
[CCBYSA]: https://creativecommons.org/licenses/by-sa/4.0/
[CCBYNC]: https://creativecommons.org/licenses/by-nc/4.0/
