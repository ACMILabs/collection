# ACMI Collection Data

**Deprecated**: this Collection archive has now been deprecated.

Please see our Collections API: https://api.acmi.net.au

The Github repository can be found at: https://github.com/ACMILabs/acmi-api

Metadata archive locations:

* `TSV` spreadsheet: [/app/tsv/works.tsv](https://github.com/ACMILabs/acmi-api/blob/main/app/tsv/works.tsv)
* `JSON` metadata: [/app/json/works/](https://github.com/ACMILabs/acmi-api/tree/main/app/json/works)

## Release and license

The dataset is released under the most open license available --- Creative Commons Zero. This brings the data in line with other releases from Europeana, Cooper Hewitt Smithsonian Design Museum, Tate, MOMA, and Digital Public Library of America (DPLA) and offers the most compatibility and clarity of use for international users.

## Data formats

The collection data is provided in an aggregate TSV file, and individual JSON files. You can find the TSV file in `src` folder labelled `collections_data.tsv`. This file uses tab-separated values, similar to a comma separated values file (CSV), and can be opened in Excel.

### Opening TSV in Excel

The TSV provided is in the following structure:

- Tab delimited
- Multi value columns use a pipe (or vertical bar) character to separate string values.
- The file is encoded in UTF-8
- The file does _not_ include a BOM (byte order mask) so that it is slightly easier to use with some scripting languages.
- This means when you open the TSV, you will likely need to set the encoding format to UTF-8.

If you are using Excel 2010, try the following steps to open the TSV file:

1. Go to _File > Open_, and browse for _All Files (*.*)_
2. Select the _.tsv_ file, this will open up the Text Import Wizard.
3. Set _Original data type_ to __Delimited__
4. Set _File origin_ to __650001 : Unicode (UTF-8)__ (on Mac, this might just say Unicode UTF-8)
5. Click Next
6. Set the Delimiter to Tab, leave the others unchecked
7. Set the Text qualifier to double quotes __"__
8. Leave _Column data format_ as __General__

If titles appear with strange characters displaying, double check that you have imported the file as __Unicode (UTF-8)__

### JSON files

Individual JSON files can be found in the `dist` folder, under `objects`. The filename and directory structure is based on the `system_id` of the object. Sub-directories are constructed by separating the object's ID into groups of three numbers or less, starting front to back. For example the full path for ***Days of Echuca*** is `/dist/objects/129/96/12996.json` (System ID# 12996). This follows the pattern used by the Cooper Hewitt, Smithsonian Design Museum in their [data release](https://github.com/cooperhewitt/collection).

## Data structure

This intial data release is a flattened version of the dataset, and many database values have been aggregated for the release. The keys for each object are:

* `abstract` - A short one line description of the work's content
* `acmi_identifier` - An internally used identifier for the record, with a non uniform pattern. In most cases, use the system_id to uniquely identify the record instead.
* `active_carriers_public_types_and_formats_only` - The format that the title is held in ACMI's collection (e.g. 16mm film, VHS, DVD)
* `audience_classification` - The formal classification from the Australian Classification Board, or the ACMI provided classification for the Mediatheque. Multiple values are pipe (|) separated.
* `colour` - Black and White, Colour, Tinted, or a combination (separated by a pipe character)
* `creation_date` - The year (or thereabouts of production). Formats include YYYY, a range is YYYY-YYYY, approximate years are Circa YYYY, or Circa YYYY-Circa YYYY. Dates with specific month will be in MMM YYYY format. Dates with date, month and year, are in DD MMM YYYY format. Some records may carry the decade.
* `creator_contributor_role` - The name of a creator and their production role in the context of this work, separated by a comma.
* `description` - Free text description of the work's content.
* `form` - The title's form (e.g. Short films). Child forms are described with its relationship to its parent, separated by a forward slash. (e.g. Short films/Short films - Great Britain).
* `genre` - The genre or genres for the title. Child genres are described with its relationship to its parent, separated by a forward slash. (e.g. Documentary/Documentary films - Great Britain).
* `language_keywords` - The primary language of any spoken content in the work.
* `length` - The length of the title in hours, minutes, seconds separated by a colon. Titles with multiple lengths will be separated by a pipe character.
* `member_object` - In a grouped title, member objects are the children of this work (e.g. Episodes of a television series).
* `object_relationship` - A description of the member object relationship.
* `other_language_notes` - Free text notes on specifics associated with `other_languages`.
* `other_language_type` - The type of secondary languages (e.g. subtitle or intertitle).
* `other_languages` - Secondary languages of any spoken content in the work.
* `other_title` - Alternative titles for the work.
* `other_title_type` - The type of alternative title for the work.
* `part_of_compilation_title_or_vod_package` - Other part of `member_object`, this is the parent of the current title.
* `permalink` - A permanent URL to this object as it appears on the ACMI collection website.
* `place_of_production` - The place (usually country) where the work was produced, Australian content may be more specific.
* `record_type` - The categorisation of the particular data structure used within the colllection management system (used administatively).
* `related_object_notes` - Free text description of the nature of the `related_objects` relationship.
* `related_objects` - Without being a part of, a relationship to another object (e.g. a sequel / prequel or a remake).
* `sound_audio` - Silent vs Sound.
* `subject_group` - The subject content of the work, grouped by topic.
* `system_id` - A unique identifier for the record, this is a reliable unique identifier for linking this ID to other systems, and it is used in constructing URLs for the ACMI collection website.
* `title` - The primary title of the work.
* `viewing_guidelines` - Discretionary warnings or notices for viewers of the work, often related to the `audience_classification` (e.g. notices that say, the following contains course language, adult themes, etc).

### Data types

| Key   | Data type |
|---|---|
| system_id | integer |
| permalink | string |
| record_type | string |
| acmi_identifier | string |
| title | string |

All other properties are ___arrays of strings___.

### Example object

```
{
    "system_id": 21100, 
    "permalink": "http://collections.acmi.net.au/objects/21100", 
    "record_type": "Title", 
    "acmi_identifier": "001342", 
    "title": "Blue pullman", 
    "other_title": [
        ""
    ], 
    "other_title_type": [
        ""
    ], 
    "place_of_production": [
        "United Kingdom"
    ], 
    "creation_date": [
        "1960"
    ], 
    "creator_contributor_role": [
        "British Transport Films, production company", 
        "British Information Services, production company", 
        "Edgar H. Anstey, producer", 
        "James Ritchie, director"
    ], 
    "colour": [
        "Colour"
    ], 
    "sound_audio": [
        "Sound"
    ], 
    "language_keywords": [
        "English"
    ], 
    "other_languages": [
        ""
    ], 
    "other_language_type": [
        ""
    ], 
    "other_language_notes": [
        ""
    ], 
    "length": [
        "00:25:00"
    ], 
    "audience_classification": [
        ""
    ], 
    "viewing_guidelines": [
        ""
    ], 
    "form": [
        "Short films", 
        "Short films/Short films - Great Britain"
    ], 
    "genre": [
        "Documentary", 
        "Documentary/Documentary films - Great Britain"
    ], 
    "subject_group": [
        "Communications, Infrastructure, & Transport/Railroad trains", 
        "Communications, Infrastructure, & Transport/Diesel locomotives - Great Britain", 
        "Communications, Infrastructure, & Transport/Railroads - Pullman cars", 
        "Communications, Infrastructure, & Transport/Railroads - Great Britain", 
        "History/History"
    ], 
    "abstract": [
        ""
    ], 
    "description": [
        "Introduces the businessman's first class express, the new 90 m.p.h. diesel Pullman. Undergoing its preliminary trials between London and Manchester, the features of the train demonstrate themselves with almost no commentary, and the final sequence shows the train in action seen from the air, and from the driver's cabin."
    ], 
    "member_object": [
        ""
    ], 
    "part_of_compliation_title_or_vod_package": [
        ""
    ], 
    "related_objects": [
        ""
    ], 
    "object_relationship": [
        ""
    ], 
    "related_object_notes": [
        ""
    ], 
    "active_carriers_public_types_and_formats_only": [
        "16mm film; Limited Access Print (Section 2)", 
        "16mm film; Preservation Print (Section 5)", 
        "16mm film; Access Print (Section 1)"
    ]
}
```

***

## Creative Commons License

# CC0 1.0 Universal

```
CREATIVE COMMONS CORPORATION IS NOT A LAW FIRM AND DOES NOT PROVIDE LEGAL SERVICES. DISTRIBUTION OF THIS DOCUMENT DOES NOT CREATE AN ATTORNEY-CLIENT RELATIONSHIP. CREATIVE COMMONS PROVIDES THIS INFORMATION ON AN "AS-IS" BASIS. CREATIVE COMMONS MAKES NO WARRANTIES REGARDING THE USE OF THIS DOCUMENT OR THE INFORMATION OR WORKS PROVIDED HEREUNDER, AND DISCLAIMS LIABILITY FOR DAMAGES RESULTING FROM THE USE OF THIS DOCUMENT OR THE INFORMATION OR WORKS PROVIDED HEREUNDER.
```

### Statement of Purpose

The laws of most jurisdictions throughout the world automatically confer exclusive Copyright and Related Rights (defined below) upon the creator and subsequent owner(s) (each and all, an "owner") of an original work of authorship and/or a database (each, a "Work").

Certain owners wish to permanently relinquish those rights to a Work for the purpose of contributing to a commons of creative, cultural and scientific works ("Commons") that the public can reliably and without fear of later claims of infringement build upon, modify, incorporate in other works, reuse and redistribute as freely as possible in any form whatsoever and for any purposes, including without limitation commercial purposes. These owners may contribute to the Commons to promote the ideal of a free culture and the further production of creative, cultural and scientific works, or to gain reputation or greater distribution for their Work in part through the use and efforts of others.

For these and/or other purposes and motivations, and without any expectation of additional consideration or compensation, the person associating CC0 with a Work (the "Affirmer"), to the extent that he or she is an owner of Copyright and Related Rights in the Work, voluntarily elects to apply CC0 to the Work and publicly distribute the Work under its terms, with knowledge of his or her Copyright and Related Rights in the Work and the meaning and intended legal effect of CC0 on those rights.

1. __Copyright and Related Rights.__ A Work made available under CC0 may be protected by copyright and related or neighboring rights ("Copyright and Related Rights"). Copyright and Related Rights include, but are not limited to, the following:

    i. the right to reproduce, adapt, distribute, perform, display, communicate, and translate a Work;

    ii. moral rights retained by the original author(s) and/or performer(s);

    iii. publicity and privacy rights pertaining to a person's image or likeness depicted in a Work;

    iv. rights protecting against unfair competition in regards to a Work, subject to the limitations in paragraph 4(a), below;

    v. rights protecting the extraction, dissemination, use and reuse of data in a Work;

    vi. database rights (such as those arising under Directive 96/9/EC of the European Parliament and of the Council of 11 March 1996 on the legal protection of databases, and under any national implementation thereof, including any amended or successor version of such directive); and

    vii. other similar, equivalent or corresponding rights throughout the world based on applicable law or treaty, and any national implementations thereof.

2. __Waiver.__ To the greatest extent permitted by, but not in contravention of, applicable law, Affirmer hereby overtly, fully, permanently, irrevocably and unconditionally waives, abandons, and surrenders all of Affirmer's Copyright and Related Rights and associated claims and causes of action, whether now known or unknown (including existing as well as future claims and causes of action), in the Work (i) in all territories worldwide, (ii) for the maximum duration provided by applicable law or treaty (including future time extensions), (iii) in any current or future medium and for any number of copies, and (iv) for any purpose whatsoever, including without limitation commercial, advertising or promotional purposes (the "Waiver"). Affirmer makes the Waiver for the benefit of each member of the public at large and to the detriment of Affirmer's heirs and successors, fully intending that such Waiver shall not be subject to revocation, rescission, cancellation, termination, or any other legal or equitable action to disrupt the quiet enjoyment of the Work by the public as contemplated by Affirmer's express Statement of Purpose.

3. __Public License Fallback.__ Should any part of the Waiver for any reason be judged legally invalid or ineffective under applicable law, then the Waiver shall be preserved to the maximum extent permitted taking into account Affirmer's express Statement of Purpose. In addition, to the extent the Waiver is so judged Affirmer hereby grants to each affected person a royalty-free, non transferable, non sublicensable, non exclusive, irrevocable and unconditional license to exercise Affirmer's Copyright and Related Rights in the Work (i) in all territories worldwide, (ii) for the maximum duration provided by applicable law or treaty (including future time extensions), (iii) in any current or future medium and for any number of copies, and (iv) for any purpose whatsoever, including without limitation commercial, advertising or promotional purposes (the "License"). The License shall be deemed effective as of the date CC0 was applied by Affirmer to the Work. Should any part of the License for any reason be judged legally invalid or ineffective under applicable law, such partial invalidity or ineffectiveness shall not invalidate the remainder of the License, and in such case Affirmer hereby affirms that he or she will not (i) exercise any of his or her remaining Copyright and Related Rights in the Work or (ii) assert any associated claims and causes of action with respect to the Work, in either case contrary to Affirmer's express Statement of Purpose.

4. __Limitations and Disclaimers.__

    a. No trademark or patent rights held by Affirmer are waived, abandoned, surrendered, licensed or otherwise affected by this document.

    b. Affirmer offers the Work as-is and makes no representations or warranties of any kind concerning the Work, express, implied, statutory or otherwise, including without limitation warranties of title, merchantability, fitness for a particular purpose, non infringement, or the absence of latent or other defects, accuracy, or the present or absence of errors, whether or not discoverable, all to the greatest extent permissible under applicable law.

    c. Affirmer disclaims responsibility for clearing rights of other persons that may apply to the Work or any use thereof, including without limitation any person's Copyright and Related Rights in the Work. Further, Affirmer disclaims responsibility for obtaining any necessary consents, permissions or other rights required for any use of the Work.

    d. Affirmer understands and acknowledges that Creative Commons is not a party to this document and has no duty or obligation with respect to this CC0 or use of the Work.
