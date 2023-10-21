# Table of Contents
0. [Sources](#0-sources)
1. [Content](#1-content)
2. [Structure Overview](#2-structure-overview)
3. [Structual features](#3-structural-features)
4. [Inline markup and transcriptional features](#4-inline-markup-and-transcriptional-features)
5. [Metadata](#5-metadata-section)
6. [Semantic markup](#6-semantic-markup)

# 0. Sources

    - Мандельштам О. Камень. Санкт-Петербург: Акме, 1913.
    - Мандельштам О. Камень. Петроград: Гиперборей, 1916.
    - Мандельштам О. Камень. Петроград: Госиздат, 1923.
    - Мандельштам О. Стихотворения. М.: Государственное издательство, 1928.
    - Мандельштам О. Стихотворения / Сост. и примеч. Н. И. Харджиева. Ленинград, 1973 (Б-ка поэта. Больш. сер.).
    - Гиперборей. 1912. № 10 (октябрь).
    - Аполлон. 1910. № 9. С. 6.
    - Firestone Library (hsvm): Box 1. Osip Mandelʹshtam Papers, 1900s-1970s (mostly 1914-1937). 
    - ИРЛИ. Ф. 428.


# 1. Content
    - ДЫХАНІЕ ("Дано мнѣ тѣло — что мнѣ дѣлать съ нимъ...")
    - SILENTIUM ("Она еще не родилась...")
    - "Невыразимая печаль..."
    - "Медлительнѣе снѣжный улей..."
    - "Смутно-дышащими листьями..."
    - "Отчего душа — такъ пѣвуча..."
    - "Быть можетъ я тебѣ не нуженъ..."
    - "Скудный лучъ, холодной мѣрою..."
    - "Образъ твой, мучительный и зыбкій..."
    - 3МѣЙ ("Осенній сумракъ — ржавое желѣзо...")
    - "Сегодня дурной день..."
    - ПѢШЕХОДЪ ("Я чувствую непобѣдимый страхъ...")
    - "Нѣтъ, не луна, а свѣтлый циферблатъ..."
    - "Я ненавижу cвѣтъ..."
    - КАЗИНО ("Я не поклонникъ радости предвзятой...")
    - ЦАРСКОЕ СЕЛО ("Поѣдемъ въ Царское Село!..")
    - ЗОЛОТОЙ ("Цѣлый день сырой осенній воздухъ...")
    - СТАРИКЪ ("Уже свѣтло, поетъ сирена...")
    - ПЕТЕРБУРГСКIЯ СТРОФЫ ("Надъ желтизной правительственныхъ зданій...")
    - "Въ душномъ барѣ иностранецъ..."
    - ЛЮТЕРАНИНЪ ("Я на прогулкѣ похороны встрѣтилъ...")
    - АЙЯ-СОФІЯ ("Айя-Софія — здѣсь остановиться...")
    - NOTRE DAME (" Гдѣ римскій судія судилъ чужой народъ...")


# 2. Structure Overview

## 2.1 Basic Structure of a Book

This TEI model based on http://www.tei-c.org/release/xml/tei/custom/schema/relaxng/tei_all.rng is designed for encoding books and includes different text versions within a single XML file. 

```xml
<TEI xmlns="http://www.tei-c.org/ns/1.0" xml:id="book_identifier">
  <teiHeader>
    [metadata]
  </teiHeader>
  <text type="Stone">
    <group>
      <text type="text1_identifier">
        <body>
          [text content]
        </body>
      </text>
      <text type="text2_identifier">
        <body>
          [text2 content]
        </body>
      </text>
    </group>
  </text>
</TEI>
```


## 2.2 Texts Within a Book

The `<group>` element wraps around multiple `<text>` elements, each having a type attribute to indicate the name of the text. Each `<text>` element includes a `<body>` that contains the actual content.

## 2.3 Book Physical Boundaries
### 2.4.1 Line Breaks
In the context of this digital edition of a book of poems, the `<lb/>` element is used to indicate line breaks in the source text.
- General Rule: Each poetic line in the source is followed by an `<lb/>` element.
```xml
    <l n="1"><lb xml:id="line_break_1"/>The first line of the poem.</l>
    <l n="2"><lb xml:id="line_break_2"/>The second line of the poem.<l>
```

- End of Page: The `<lb/>` element is not used at the end of a page.
- No Hyphens: Hyphenation marks are not applicable in this context.

### 2.4.2 Page Divisions

Each page of the original text is represented as a separate `<div>` element within the `<body>` of the `<text>` element. The type attribute of the `<div>` indicates the page number or some other identifier.

For example:


```xml
<text type="3МѣЙ">
  <body>
    <div type="1">
      <!-- Content of the first page -->
      <pb ed="#K1" n="K1_12"/>
    </div>
    <div type="2">
      <!-- Content of the second page -->
      <pb ed="#K1" n="K1_13"/>
    </div>
  </body>
</text>
```


### 2.4.3 Page Breaks

Page breaks are encoded using the `<pb/>` tag.
Attributes:

- `n`: This mandatory attribute contains the image's file name that represents the page, excluding the file extension.
- `ed`: This optional attribute specifies the edition to which the represented page belongs.

Example:

`<pb n="K1_12" ed="#K1"/>`

In this example, the n attribute indicates that the image file for this page is named "K1_12" (without extension), and the ed attribute indicates that this page belongs to the edition identified by "#K1".

# 3. Structural features

## 3.1. Verses

Here is a verse `</l>`

## 2.2 Stanzas and other grouping of verses

```xml
<lg>
    <head>Title of a poem</head>
    <l>a verse</l>
    <l>a verse</l>
    <l>a verse</l>
    <l>a verse</l>
</lg>
```


## 3.3 Rhyme Tag

The `<rhyme>` element is used to denote rhyming words within verses. It has a label attribute to indicate the type of rhyme.

Example:
```xml
    <l n="1"><lb xml:id="OM_kamen_lb_1913_03_01"/>Дано мнѣ тѣло — что мнѣ дѣлать <rhyme label="a">съ нимъ</rhyme>,</l>
    <l n="2"><lb xml:id="OM_kamen_lb_1913_03_02"/>Такимъ единымъ и такимъ <rhyme label="a">моимъ</rhyme>?</l>
```

In this example, the words "съ нимъ" and "моимъ" are marked as rhyming words and are both labeled with "a" to indicate that they form a rhyming pair.

# 4. Inline markup and transcriptional features
## 4.1 Encoding of Witnesses

Witnesses to textual variations are encoded within the `<app>` element. The `<app>` element can appear both in the <head> and within individual lines (`<l>`).
Attributes:

- `resp`: Specifies the person responsible for the apparatus entry. For example, `resp="#maria"`.

Child Elements:

- `<lem>`: The lemma, or the "original" reading, which is accompanied by wit attributes listing the witnesses that support this reading. For example, `<lem wit="#K1 #K2 #K3 #C #BP">SILENTIUM</lem>`.
- `<rdg>`: Stands for "reading" and represents a variant reading. It also has a wit attribute listing the witnesses that support this reading. Optional attributes like type and cause can be used to specify the nature of the variant. For example, `<rdg wit="P">XIII</rdg> or <rdg cause="om" wit="#A"/>`.

Example:
```xml
<head>
  <app resp="#maria">
    <lem wit="#K1 #K2 #K3 #C #BP">SILENTIUM</lem>
    <rdg wit="P">XIII</rdg>
    <rdg cause="om" wit="#A"/>
  </app>
</head>
<l n="1">
  <lb/>Она еще не <rhyme label="a">родилась</rhyme>
  <app>
    <lem wit="#K1 #K2 #K3 #C">,</lem>
    <rdg type="subs" wit="#A">—</rdg>
  </app>
</l>
```

In this example, the lemma "SILENTIUM" is supported by witnesses #K1, #K2, #K3, #C, and #BP. A different reading "XIII" is supported by witness P. There is also a reading that is omitted (om) in witness #A.

## 4.2 Facsimile Markup for Text-Image Alignment

This section is crucial for linking the digital text to its corresponding physical representation in an image. The semantic markup here serves as a bridge between the textual and visual elements.
- `<facsimile>`
    - `xml:id`: Unique identifier for the facsimile.

- `<surface>`
    - `corresp`: Corresponds to a particular part of the textual content.
    - `xml:id`: Unique identifier for the surface.

- `<graphic>`
    - `url`: Path to the image file.
    - `width`, `height`: Dimensions of the image.

- `<zone>`
    - `xml:id`: Unique identifier for each zone.
    - `lry`, `lrx`, `uly`, `ulx`: These attributes define the coordinates of the bottom right and upper left corners of each line or "zone" in the image.
    - `rendition`, `rend`: Specifies the visual characteristics, like visibility.
    - `corresp`: Links the zone to a specific line in the text.

In the text, the attribute `facs` is used to reference a specific zone in the image, thereby aligning the digital text with its visual representation. The `app` and `lem` elements further enrich this alignment by capturing textual variations.

Example facsimile markup:
```xml
<zone xml:id="OM_kamen_line_1913_03_12" lry="748" lrx="348" uly="726" ulx="74" rendition="Line" corresp="#OM_kamen_lb_1913_03_12" rend="visible"/>
```

Example text markup:
```xml
<l n="12"><lb facs="#OM_kamen_line_1913_03_12" n="12" xml:id="OM_kamen_lb_1913_03_12"/>Узора милаго не зачеркнуть. 
```

# 5 Metadata Section

The metadata section is enclosed within the `<teiHeader>` element and consists of several sub-elements that describe the document and its creation details.

## 5.1 Publication Statement
- `fileDesc`: This is the file description container.

- `titleStmt`: Statement of responsibility for the digital edition.
    - `title`: The title of the project.
    - `author`: The author of the original work, represented in different languages (`xml:lang` attribute).
    - `respStmt`: Statement of editorial responsibility.
    - `resp`: Specifies the type of responsibility.
    - `name`: The name of the person responsible, with an `xml:id` attribute.

- `editionStmt`: Edition statement.
    - `edition`: Description of the edition and its goals.
    - `note`: Additional notes about the project.
    - `date`: Publication date of the digital edition.
    - `interpGrp`: Group of interpretative notes. Each `interp` element has an `xml:id` attribute for identification and contains textual content explaining the source.
  - `extent`: Describes the size of the digital file (in kilobytes).

- `publicationStmt`: This is the publication statement.
    - `authority`: The name of the project or organization responsible for the publication.
    - `date`: The year of publication.
    - `availability`: Availability status of the digital edition. Text specifying the license and usage permissions.
    - `ref`: Link to the license (Creative Commons Attribution 4.0 International License in this example).

## 5.2 Source Description Section

The `sourceDesc` element contains a detailed description of the sources being represented.

### 5.2.1 Physical description
- `msDesc`: Book description container.

    - `msIdentifier`: Identifies the book.
        - `settlement`: The city where the book is kept.
        - `repository`: The repository holding the book.
        - `idno`: The specific identification number for the book.

    - `msContents`: Information about the contents.
        - `summary`: A summary of the book's significance and various editions.
        - `textLang`: Information about the language of the text.
        - `msItem`: Detailed list of individual poems.
        - `locus`: Specifies the location (usually page numbers).
        - `title`: Title of the poem, with type and subtype attributes.

    - `physDesc`: Physical description of the book.
        - `objectDesc`: Description of the object's form.
        - `supportDesc`: Information about the material.
        - `support`: Description of the material and binding.
        - `extent`: Number of leaves and dimensions.
    - `layoutDesc`: Layout description.
        - `layout`: Specifies the design, like the number of columns.

    - `history`: Historical context.
        - `origin`: Initial publication information.
        - `provenance`: History of revisions and re-publications.

### 5.2.2 Witnesses description
The `listWit` element contains a list of witnesses for a particular version of the text. It is identified by `xml:id` and `ana` attributes, and the responsible party is indicated by the `resp` attribute.
- `head`: The head element provides a title for the list.
- `witness`: The witness element describes individual witnesses.
    - `xml:id`: Identifier for this witness.
    - Text Content: A textual description or name of the witness.
- `msDesc`: Similar to the earlier msDesc, but nested within witness. Provides additional details specific to this witness:
    - `msIdentifier`
        - `settlement`: Specifies where the book or manuscript is located, here it's "Princeton University Library."
        - `repository`: The specific part of the library, "Firestone Library (hsvm): Box 1."
        - `collection`: Name of the collection to which the book or manuscript belongs.
        - `idno`: Identification number, "C0539."
        - `altIdentifier`: Alternate identification, such as a URL.

Example:
```xml
<listWit xml:id="rec1_wits" ana="#rec1">
    <head>Witnesses of version A</head>
    <witness xml:id="P">Принстонский архив Мандельштама
        <msDesc>
            <msIdentifier>
                <settlement>Princeton University Library</settlement>
                <repository>Firestone Library (hsvm): Box 1</repository>
                <collection>Osip Mandelʹshtam Papers, 1900s-1970s (mostly 1914-1937)</collection>
                <idno>C0539</idno>
                <altIdentifier>
                    <idno>https://findingaids.princeton.edu/catalog/C0539_c185</idno>
                </altIdentifier>
            </msIdentifier>
        </msDesc>
    </witness>
</listWit>
```
This section helps trace the provenance and location of specific versions or witnesses of the text.

### 5.2.3 Encoding information
- `encodingDesc`: This section defines the guidelines and principles followed in the digital encoding of the text.
  - `editorialDecl`: Specifies editorial practices applied to the text:
      - `correction`: Indicates that no modifications have been made to typos or inconsistencies in the original paper edition.
      - `normalization`: States that the text is transcribed without normalization, preserving the old Russian orthography.
      - `segmentation`: Describes how the text is segmented, stating it follows the original paper layout without additional divisions.
      - `hyphenation`: Specifies that the original paper edition's poetry did not contain hyphens due to line breaks, and this convention is maintained in the digital version.

  Each element contains a `<p>` tag with a detailed description of the editorial practice.
  - `variantEncoding`
      - `method`: Describes the encoding method used for textual variants, which is "parallel-segmentation" in this case.
      - `location`: Indicates where the variant text is located, which is "internal" here. This means that all variants are encoded within the same file or document.

  The `encodingDesc` provides critical meta-information that helps users understand the editorial choices made during the digital transcription.

- `profileDesc`: This section contains contextual information about the text.
    - `langUsage`
        - `language`: Specifies the language of the text, which is Russian in this case. It also notes that the text uses old Russian orthography.

- `revisionDesc` Section: This section logs changes made to the document:
    - `change`: Describes a significant revision to align the markup with the latest TEI guidelines.
    - `when`: Indicates the date of the change, which is October 2023.
    - `who`: Specifies who made the change, denoted by the initials "ML".

`profileDesc` and `revisionDesc` provide useful metadata about the language usage and the history of changes in the document.

# 6 Semantic markup
## 6.1 List of persons
This section is designed to annotate persons mentioned in the text semantically.
- `person`
    - `xml:id`: Unique identifier for the person.
    - `sameAs`: Provides a reference to an external database, in this case, DBpedia.
    - `persName`: Lists the person's name in different languages (English, Russian, Italian).
    - `idno`: Provides an identifier from an external authority (VIAF).
    - `birth` and `death`: Specifies the birth and death dates and places.
        `when`: Date of the event.
        `placeName`: Geographical location.
    - `affiliation` `listRef`: Lists affiliations of the person over time.
        - `ref`: Each affiliation includes:
        - `orgName`: The name of the organization.
        - `address`: The location of the organization.
        - `date`: The period during which the person was affiliated with the organization.

Example:
```xml
 <person xml:id="p_Mandelstam" sameAs="http://dbpedia.org/resource/Osip_Mandelstam">
    <persName xml:lang="en">Osip Emilyevich Mandelstam</persName>
    <persName xml:lang="ru">Осип Эмильевич Мандельштам</persName>
    <persName xml:lang="it">Osip Ėmil'evič Mandel'štam</persName>
    <idno type="VIAF">https://viaf.org/viaf/102337271/</idno>
    <birth when="1891-01-02">
        <placeName>Warsaw, Congress Poland, Russian Empire</placeName>
    </birth>
    <death when="1938-12-27">
        <placeName>Vtoraya Rechka transit camp, near Vladivostok, Russia, USSR</placeName>
    </death>
    <affiliation>
        <listRef>
            <ref>
                <orgName>Tenishev School</orgName>
                <address>
                    <addrLine>St. Petersburg, Russia</addrLine>
                    </address>
                    <date>1900-1907</date>
            </ref>
            <ref>
                <orgName>Sorbonne</orgName>
                <address>
                    <addrLine>Paris, France</addrLine>
                </address>
                <date>1908-1909</date>
            </ref>
            <ref>
                <orgName>University of Heidelberg</orgName>
                <address>
                    <addrLine>Heidelberg, Germany</addrLine>
                </address>
                <date>1909-1911</date>
            </ref>
            <ref>
                <orgName>University of Saint Petersburg</orgName>
                <address>
                    <addrLine>Saint Petersburg, Russia</addrLine>
                </address>
                <date>1911-1917</date>
            </ref>
        </listRef>
    </affiliation>
</person>
```

## 6.2 List of places

This section is designed to semantically annotate places mentioned in the text.
- `place`
    - `xml:id`: Unique identifier for the place.
    - `sameAs`: Reference to an external database, here, DBpedia.
- `placeName`
    Provides the name of the place in different languages (English, Russian, Turkish).
- `location`
    `geo`: Specifies the geographical coordinates (latitude and longitude).
- `desc`
    A description that provides historical and contextual information about the place.
- `country`
    Specifies the country where the place is located.

This semantic markup provides comprehensive information about Hagia Sophia, detailing its names in different languages, its geographical location, historical context, and its country in a structured format.

Example:
```xml
<place xml:id="p_hagia_sophia" sameAs="http://dbpedia.org/resource/Hagia_Sophia">
    <placeName xml:lang="en">Hagia Sophia</placeName>
    <placeName xml:lang="ru">Айя-София</placeName>
    <placeName xml:lang="tr">Ayasofya</placeName>
    <location>
        <geo>41.0086 28.9802</geo>
    </location>
    <desc>Hagia Sophia is a former Greek Orthodox Christian basilica, later an imperial mosque, and now a museum in Istanbul, Turkey. Built in AD 537, it was the world's largest building and an engineering marvel of its time. It is considered the epitome of Byzantine architecture and is said to have "changed the history of architecture."</desc>
    <country>Turkey</country>
</place>
```

## 6.3 Bibliography list
This section provides a structured list of bibliographic references related to the text.
- `bibl`
    - `type`: Specifies the type of bibliographic entry, such as "work."
    - `xml:id`: A unique identifier for each bibliographic entry.
    - `sortKey`: Key used for sorting the entries.
    - `title`: Provides the title of the work in different languages and types (e.g., short, long).
    - `author`: Specifies the author of the work, linking to their XML ID for more information.
    - `relatedItem`:  Links to another bibliographic entry that is related to the current one, using the target attribute.
    - `date`: Specifies the publication date of the work.

This semantic markup captures detailed bibliographic information in a structured manner, making it easier to manage and query.

Example
```xml
<bibl type="work" xml:id="w_lekmanov" sortKey="Sobranie_soch">
    <title xml:lang="ru">Собрание стихотворений</title>
    <title type="short" xml:lang="it">Собрание стихотворений 1906—1937 / Осип Мандельштам; сост. О. А. Лекманова, М. А. Амелина, предисл. О. А. Лекманова, коммент. и библиогр. О. А. Лекманова, Е. А. Глуховской, А. А. Чабан. — М.: Ру- тения, <date>2017</date>. — 560 с., ил.</title>
    <author ref="#p_Mandelstam" xml:lang="ru">Осип Мандельштам</author>
</bibl>
```