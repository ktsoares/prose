---
title: Release Notes
---
{% include toc.liquid.md %}

## Release 7.5.1 -- 2019/11/26

- General
  - Fixed bug that made PROSE not work on .NET Core 3.x.   
- Extraction.Text
  - Allowed implicit/nullable examples.
  - Supported customized columns in table example.
- Extraction.Spreadsheet
  - Implemented first version of ranking algorithm, so the top suggested table is the desired one in most cases.

## Release 7.4.0 -- 2019/10/28

- General
  - The PDBs included in our nuget packages are now "Full" PDBs for net45 and net46 but still "Portable" PDBs for CoreClr.
- Extraction.Text
  - Implemented branch and bound ranking.
- Transformation.Tree
  - Improved ranking of synthesized programs.
- Extraction.Web
  - Improved and more expressive row selector inference.
  - Simpler HTML table selectors with shorter path expressions/fewer disjuncts.

## Release 7.3.0 -- 2019/09/23

No substantial changes since the last public release.

## Release 7.1.0 -- 2019/08/29

- Transformation.Text
  - Improved readability of generated Python code based on simplification of used regular expressions.
  - Fixed an issue with Date/Time programs where the hour value is 24 (which technically isn't a valid time, but could
    be considered hour 0 of the next day).
- Extraction.Json
  - Generated code for pandas and PySpark is now a snippet instead of a function; hence, Get{Pandas,Pyspark}Code methods
    do not have functionName parameter any more.
- Extraction.Text
  - Implemented Python translation.
  - Generated readable step names for Extraction.Text's PowerQuery M translation.
  - Added encoding option for M code generation.
  - Added learning exception.
- Nuget packages now contain PDB files that match the assemblies.

## Release 7.0.0 -- 2019/07/30
- New Extraction.Text
  - Existing implementation renamed to Extraction.Text.Deprecated, new implementation returns tables rather than
    hierarchical results and is designed to support readable translation to both M and Python.
- Transformation.Text
  - Improved python translation for datetime programs
  - Added support for synthesis of programs that perform rounding on years
- Compound.Split
  - Added `ColumnNamesCleaning` parameter to `RunClean` methods, used to specify the way column names are cleaned.
  - Changed delimiter learning so that learned delimiter can be overriden by specifying `DelimiterStrings` (with a
    single delimiter) together with `SimpleDelimiter` or `SimpleDelimiterOrFixedWidth` constraints.
- Security fix:
  - Java dependency (used only for PROSE programs translated to java) Jackson-databind updated to version 2.9.9.1
- Detect.DataTypes
  - Improved fail-fast performance.
- Transformation.Tree
  - Added method to pretty print programs
- Matching.Text
  - Python translations now include outlier examples in the comments
- Split.Text
  - Added `ProvidedQuotingConfigurations` to `Witnesses.Options`, which specifies quoting configurations used for
    learning.
  - Changed learning so that it returns non-contextual single delimiter programs with `DelimiterStringsConstraints` and
    `SimpleDelimiter` or `SimpleDelimiterOrFixedWidth` constraints.


## Release 6.20.1 -- 2019/06/24

### Bug Fixes / Enhancements

- Extraction.Web: 
    - Remove dependence on href attributes in eWeb learning as this can cause overfitting.
- Transformation.Tree:
    - Remove on the fly synthesis.
- Transformation.Text:
    - Improved readability of translation of date time parsing programs.

## Release 6.20.0 -- 2019/05/29

### New Features

- Data.Diff is a new package for computing differences in data distributions -- currently supports the 1D numerical case
  and the simplest categorical case.

### Bug Fixes / Enhancements

- Compound.Split
  - Added performance optimizations to learning.
- Detection
  - Now depends on the ExcelDataReader NuGet package.
- Extraction.Web
  - In predictive mode, include columns that are supersets of other columns when both granularities could make sense.
  - When learning a new selector, prefer previously learned column selectors if they satisfy the global alignment even
    if the newly learned selectors also satisfy the examples for those columns.
- Split.Text
  - Added performance optimizations to learning.

## Release 6.18.0 -- 2019/04/11

### New Features

- Extraction.Web
  - Inner text excludes script/style tag contents.

### Bug Fixes / Enhancements

- Compound.Split
  - Improved learning of quoted strings.

## Release 6.17.0 -- 2019/03/15

### New Features

- Detection.DataType
  - Implemented entity validators for e-mail addresses, IPv4 and IPv6 addresses, geographic coordinates (Lat/Lng), US
    zip codes, and US phone numbers.

### Bug Fixes / Enhancements

- Compound.Split
  - Allow learning even when the last record is trimmed by ignoring the last record during learn.
- Extraction.Web
  - Added performance optimizations to learning.
- Matching.Text
  - Fix pattern order in generated programs.
- Transformation.Text
  - Improved readability of Python translation, including regular expressions and number format simplifications.

## Release 6.14.6 -- 2019/02/15

### New Features

-	Transformation.Tree
    - Supports learning transformations “on the fly” by watching user edits.
    - Supports negative examples.

### Bug Fixes / Enhancements

-	Along with .NET 4.5 and .NET core binaries, the nuget packages now include binaries for .NET 4.6.
-	Extraction.Web
    - Multicolumn task learning now falls back to predictive programs and ensures consistency with previous program
      constraints.
    - Improved ranking of predictive tables by taking into account image nodes.
    - Exclude tables from result that are duplicate or sub-tables of other tables.
    - Ordering of table column and exclude duplication columns.
    - Improved title detection.
    - LearnTopK now supports an optional timeout.
- Matching.Text
    - Miscellaneous bug fixes.
-	Transformation.Text
    - Python readable translation now supports programs involving datetime parsing with formats that do not map directly
      to posix.
    - Python readable translation better handles regex matching when tokens do not overlap and other simplification
      rules.
    - Python readable translation is less aggressive about inlining expressions making for much more readable code.
    - Improved performance of the interpreter.

## Release 6.11.0 -- 2019/01/16

### New Features

- Extraction.Web
    - Added HTML table title recognition.
    
### Bug Fixes / Enhancements

- Extraction.Web
    - Support providing predictively learned programs as a constraint to be passed into by-example learn calls to
      improve performance and prevent needing to re-learn predicatively learned programs.
- Transformation.Text
    - Improved Python translator to support ToSimpleTitleCase, EndsWith conditions, further Datetime programs, regex
      pair matches and number transformations.

## Release 6.10.0 -- 2018/12/17

### New Features

- Compound.Split
    - Added support to read CSV/FW files with "junk rows"; that is, repeated headers and non-data, non-comment rows,
      anywhere in the file. This is not enabled by default, but rather by adding the newly introduced
      `AllowRowFiltering` constraint.
- Detection.DataType
    - Add alternate, more efficient entry point for completing the task of performing datatype detection and conversion
      on a specific data set rather than generating code for doing so.
    - Make the Python code generator available in the C# SDK.

### Bug Fixes / Enhancements

- Compound.Split
    - Improve handling of comments and empty records.
    - Added support to learn a row-selector, which can now be potentially different from the first column selector.
- Extraction.Web:
    - Learning now integrates top-down (by example) synthesis with bottom-up (predictive learning with zero examples)
      synthesis, which improves the quality of the tables extracted from web pages
- Transformation.Text
    - Support new Python translation parameter OptimizeFor.StrongReadability that gives more flexibility to the
      translator to produce more readable code by removing error handling.
- Transformation.Tree:
    - Node construction adds parent field during object creation, instead of after it.
    - Refactored the grammar to merge predicates related to the current node, parent node, and children.


## Release 6.9.0 -- 2018/11/16

### Breaking changes

- Compound.Split
    - Hides the ReadInputLineCount constraint and instead users can specify no. of lines to read while adding inputs.
    
### New Features

- Transformation.Text
    - Generate readable python code for Lookup() semantics operator.
- Extraction.Web
    - Parametrized the SimplePrograms constraint by program input and output type, allowing it to be used for any kind
      of program (field extraction, sequence extraction, etc).
    
### Bug Fixes / Enhancements

- Detection.DataType 
    - Better handling of integer columns that look like categorical data, and handling of “NaN” values in string
      columns.
    - Various bugfixes, including improving datatype detection, including non-separated dates (“20120513”) and numbers
      in parenthesis (“(45,345)”), and other improvements to parsing ambiguous date formats.
    - Enhancements to generated Python code for datatype detection.
- Core Framework 
    - Improvement to how variable substitution is done for external grammars (relevant for DSL authors).
- Compound.Split
    - Better handling of CRLF escape characters.
- Extraction.JSON
    - Bug fixes for Python code generation to prevent unnecessary column aliases: col("color") instead of
      col("color").alias("color").
- Transformation.Text
    - Bug fixes to entity detection.
    - Readability enhancements to Python translation.
- Matching.Text
    - Generate better regex to match newlines.
    - Minor bug fixes.
- Transformation.Tree
    - Fix a bug where learning on large input could lead to StackOverflow.
        

## Release 6.8.1 -- 2018/10/18

### Breaking Changes

- Compound.Split
    - `ReadInputFromReaders(TextReader reader)` and `ReadInputLineCount(int limit)` are deprecated. They are replaced by
      `ReadInput(TextReader reader, int linesToRead=200)`. This release also introduces `ReadInput(string s, int
      linesToRead=200)`.

-   Extraction.Json
    -   Removed the optional `JPath` parameter from the constraint `JoinSingleTopArray` – the new constraint `JoinArray`
        should be used instead.

### New Features

-   Common Framework
	-   New learning/running exception hierarchy to raise friendlier exceptions.

-   Detection.DataType
	-   Support added to specify the list of types to detect.

-   Extraction.Json
	-   Added new interactive constraints `Delete`, `SplitArray`, and `JoinArray`.
    -   Support added to detect JSON that have comments and unquoted property names so code generation can fail in
        unsupported targets.

-   Transformation.Text
	-   Introduce readable translation for number formatting and lookup programs.

-   Transformation.Tree:
    -   `Node.Value` of type `string` has been replaced by `Node.Attributes` of type `Dictionary<string, string>` to
        permit learning from distinct attributes.

### Bug Fixes / Enhancements

-   Detection.DataType
	-   Various bug fixes and enhancement.

-   Extraction.Json
	-   Improved flattening of embedded arrays in new-line delimited JSON (NDJSON) files.

-   Split.Text
	-  	Various performance improvements to program learning and execution.

-   Transformation.Tree:
	-   Various bug fixes.


## Release 6.7.0 -- 2018/09/20

### New Features

- Common framework
    - Configurable equality for `FeatureCalculationContext`; Classes implementing `IFeature` can now force deep/shallow
      equality computation over inputs leading to potential performance improvements during learning by setting
      `IFeature.UseComputedInputsForFccEquality` (`false` is the old behavior).

- Compound.Split
    - Support free-form fixed-width schema.
    - Add `SkipLinesCount` constraint to manually specify number of header lines to skip instead of learning it.

- Matching.Text
    - Support added for learning with `InSameCluster` and `InDifferentCluster` constraints which take a set of inputs to
      be required to appear in the same or different clusters respectively.
    - Support added for `UseLongConstantOptimization` constraint which aggressively generates constant tokens whenever
      possible. (Note: This makes the learning incompelete.)

### Bug Fixes / Enhancements

- Common framework
    - Optimizations and style improvements in quality of generated Python code.

- Compound.Split
    - Bug fixes in fixed-width file ingestion.
    - Correctly handle fixed-width files where all lines start with whitespace.
    - Fixes to Python translation.

- Extraction.Text
    - Improved learning performance in the presence of negative constraints. This fixes the performance regression
      introduced in 6.6.0.

- Extraction.Json
    - Fix handling of JSON with a single array of values in pandas Python translation.

- Extraction.Web
    - Improvements in predictive table detection to remove certain kinds of redundant columns.
    - Improved row selector inference based on ancestor nodes rather than just the boundary nodes.


## Release 6.6.0 -- 2018/08/20

### Breaking Changes

- Compound.Split
    - The property `FieldStartPositions` has been removed and a new `IReadOnlyList<Record<int, int?>> FieldPositions`
      property has been added in its place.

### New Features

- Common Framework
    - Support for serialization and deserialization of spec objects (used to track subtasks during synthesis).

- Compound.Split
    - Support for fixed width files with gaps between fields.
    - Improvement in column name learning for some cases (e.g. single column and single row data sets).
    - Support for generating PySpark code from learned program.

- Detection
    - Support for rich datatype detection on CoreClr (in addition to .net framework where it was previously supported).
    - Includes example values for each detected numeric and date type in the data.

- Extraction.Json
    - Supports a new constraint which may be used to disable handling of invalid JSON.  This constraint should be
      specified if clients translate learned programs to Java and use that java with a Jackson library version less than
      v2.8 since otherwise the generated Java code contains Jackson v2.8+ features.  (NOTE: This version of Jackson is
      particularly significant since Spark currently only allows Jackson v2.8.)
    - Support for generating PySpark code from learned program.

- Extraction.Web
    - Updated AngleSharp dependency to its latest release to address security concerns in that library.
    - Support for explicit HTML tables when run in predictive mode.

- Matching.Text
    - Includes examples of each pattern in comments next to the pattern in the generated Python code.

- Transformation.Text
    - Support for serialization and deserialization for all types referenced in the grammar.

### Bug Fixes / Enhancements

- Common Framework
    - Bug fixes in ProgramSet.TopK(k) method to return no less than k programs. Temporarily, this slightly degrades
      Extraction.Text learn performance, which will be fixed soon.

- Extraction.Json
    - More consistent handling of invalid/truncated Json files.

- Matching.Text
    - Improvements in PySpark translation

- Transformation.Text
    - Improvements in readability of generated Python code

- Transformation.Tree:
    - Performance improvement in clustering of transformations by up to 10x depending on scenario.
    - Performance improvement using incremental learning such that previously learned programs are updated with newer
      examples provided on subsequent Learn() calls.

## Release 6.5.0 -- 2018/07/23

### New Features

- Extraction.Web:
    - Now supports predictive table extraction from webpages (that is, from 0 examples).

### Bug Fixes / Enhancements

- Common framework:
    - Added support for a common extension hook for custom entity detectors.  This hook is currently used in 
      Extraction.Web and Transformation.Text but could theoretically be supported in any DSL. 
- Compound.Split:
    - Now supports fixed-width schema files which are themselves delimited.
- Detection:
    - Fixed a bug where running detection on a set of empty strings produced a NullReferenceException.
    - Fixed a bug where numbers of the form \d+\.\d+ were not recognized correctly.
- Extraction.Json:
    - Added a parameter to enable/disable support for trailing commas in java translation.  The library we use for json
      parsing in java (Jackson) has support for trailing commas in newer versions, but some environments only allow the
      older version of Jackson which does not have this support.
    - Now has a new constraint to automatically flatten a json document.  When this constraint is used, it’s possible to
      translate the learned program to python which builds on the pandas library.
- Extraction.Web:
    - Improved nth-child selection ranking in predictive extraction.  Nth-child selection is important for detecting
      table columns in some cases, but in others it can introduce a lot of noise.  The system now uses nth-child
      selection only as a fall-back if prominent tables cannot be detected otherwise.
    - Text normalization (which currently ensures that text to node matching is whitespace insensitive) has been
      extended to insensitivity of other special characters such as variations in quotes, dashes, ellipses, etc.
- Transformation.Text:
    - Readability of python translations is improved in some cases by removing unnecessary wrapping functions/classes.
    - Python translator now creates much more readable translations for programs including date time rounding.

## Release 6.4.0 -- 2018/06/26

### Breaking Changes

- Common Framework
    - When running on CoreClr, we now require runtime version 2.0.3 or newer.  Previously we had workarounds for a
      CoreClr bug that was fixed in 2.0.3, but those are now removed. 
- Compound.Split
    - Learning fixed width programs from a schema file is now specified by a constraint which contains a schema file
      parameter.
- Extraction.Json
    - New default behavior not to automatically join inner arrays.  The old behavior may be requested by supplying the
      new constraint ‘JoinInnerArrays’.  (Previous constraint ‘NoJoinInnerArrays’ has been removed.)
    - Inputs can now be used as an implicit flatten constraint, and the old explicit FlattenDocument constraint is
      removed.
    - Flattening top-level arrays is only applied when there is only one.  If multiple top-level arrays are present,
      they are all preserved.
    - Constraints are renamed to make their meaning clearer:
        - JoinInnerArrays -> JoinAllArrays
        - NormalizeArrays -> JoinSingleTopArray
        - SplitTopArrayToColumns -> SplitTopArrays

### New Features

- Common Framework
    - VSA data structures now support Serialization and Deserialization
- Compound.Split
    - Now handles small fixed-width files.
    - Now supports selecting a subset of columns for the output.
- Detection:
    - Data type detection now supports detecting bit types.
    - Data type detection now takes a CultureInfo parameter and supports identifying a type from multiple string
      values—not just one.
    - Improved data type detection algorithms have been implemented for numbers, dates, Booleans and categorical values.
- Extraction.Json
    - Now supports trailing commas.

### Bug Fixes / Enhancements

- Compound.Split
    - Improved learning of header/skip.
    - It is now possible to construct a program from a ProgramProperties structure (which can be extracted from a
      learned program).
    - It is also now possible to override some learned properties.  This supports the scenario where a program is
      learned from an input file, metadata is presented to the user, and then the user can override some of that
      metadata before using a final program based on the modified properties.
- Extraction.Json
    - New NormalizeArray constraint which directs the system to flatten only one array—either with a specified path or
      the first, top array if no path is specified.
- Extraction.Web
    - Now supports specialized selectors for HTML tables to ensure they are always handled when possible.
    - Dashes are no longer escaped in CSS selectors making them more readable.
    - Now supports boundary-based semantics for row-selectors in web table programs.
    - Increased maximum allowed offset for satisfying examples to 5.
    - Row selectors may now satisfy examples up to the maximum permitted offset if an exact match cannot be found.
    - Previous program constraint is now used to ensure partial success—that is we always satisfy any previously
      satisfied columns for which the examples have not changed (in preference to success on any new columns).
    - When new examples are given in a session where a learn was previously performed, if the new program no longer
      satisfies previously satisfied columns, we now consider those columns satisfied if the previous column examples
      shift by less than some number of rows specified as a threshold in the public API.  If they aren’t satisfied at
      all or the shifting is greater than that number of rows, then the system falls back to the previously learned
      program to ensure that the previously satisfied columns are still satisfied.
    - An issue was fixed so that we now ensure correct alignment when the row selector has been previously computed.
- Matching.Text
    - Fixed a bug in the python translation which didn’t properly quote regexes.
- Split.Text
    - Improved detection of time expressions.
- Transformation.Text
    - Python translation no longer exposes the Substring type unless optimizing for performance in order to simplify the
      generated code.
    - Python translation now special cases a common idiom in the translation.text DSL related to regex matching and
      turns it into simpler code.
    - Improved readability of python translation for some datetime programs.
    - Generated programs that use regular expressions now contain simpler/easier to read expressions in a number of
      cases.
- Transformation.Tree
    - Performance improved.
    - Fixed an issue in the Order By conversion.
    - Fixed issues with the generation of join expressions.
    - Table name analysis is now more robust with respect to qualified names, cases and quoted names.
    - Program now exposes separate methods for finding the nodes that should be changed and for performing the
      transformation instead of just doing the whole operation in a single method call.

## Release 6.3.0 -- 2018/05/15

### Breaking Changes

- Matching.Text
    - ForbidConstantTokens constraint has been removed.
- Transformation.Tree
    - Utils.Parse has been renamed to Utils.ParseStatementIgnoreWhiteSpace
    
### New Features

- Compound.Split
    - Key/Value extraction now supports fixed width extraction such as where the keys and values are in a table where
      the values all start at the same column position.
    - Now supports skipping empty, comment and footer records.
- Transformation.Text
    - Now supports pluggable Entity Detectors specified in a constraint.

### Bug Fixes / Enhancements

- Common Framework
    - PROSE now depends on a slightly older version of Newtonsoft.Json (v9.0.1) for .Net Framework consumers.  For
      .Net Core PROSE still requires Newtonsoft.Json v10.0.3.
    - Code produced by the Java translation now makes fewer allocations in some scenarios.
    - Our Python translation now produces more readable string literals.
- Compound.Split
    - The Python produced for cases which pandas cannot handle is improved with function names and parameters that
      align with pandas, documentation on public parts and simpler generated code.
- Extraction.Web
    - When learning a new program, soft constraints are now used for any columns where the user has not changed the
      examples instead of only if the user has added new columns but not changed examples for any previous columns.
    - Significant improvement in learn times.
    - Text comparisons are now insensitive to whitespace characters.
- Transformation.Text
    - Python translation is now more readable in many cases.
- Transformation.Tree
    - DSL rewritten to support additional scenarios.
    - The Program class now has a field to expose a list of learned transformation rule programs. Each transformation
      rule exposes an Edit program. In this way, users can pick which of the learned edits  they want to apply and
      apply them to specific nodes bypassing the filter checking.
    - Performance improvements.

## Release 6.2.0 -- 2018/04/25

### Breaking Changes

- Matching.Text
    - The `Patterns` property has been removed.  Patterns should be retrieved by calling the `LearnPatterns()`
      method on the session object instead.

### New Features

- Changes that only affect those building their own DSLs
    - The [Samples](https://github.com/microsoft/prose) contain a new DSL Authoring tutorial.

### Bug Fixes / Enhancements

- Compound.Split
    - The system now attempts to learn an ingestion program that obeys standard CSV quoting first
      and then falls back to the more flexible strategy only if the standard doesn’t work.
- Extraction.Web
    - Fixed bugs with case insensitive comparisons and normalization.
- Matching.Text
    - Fixed a bug in the handling of cancellation tokens.  Now we check for cancellation much more frequently.
    - Fixed handling of null strings.
    - Improved readability and performance of python translations.
- Transformation.Text
    - Significant inputs has improved performance and accuracy.
- Common Framework
    - The interface for implementing a subprogram translator has been enhanced.

## Release 6.1.0 -- 2018/04/16

### New Features

- Compound.Split
    - Can now extract the schema of a fixed width file from a free-form text file description of the schema and use that
      to learn an extraction program.

### Bug Fixes / Enhancements

- Compound.Split
    - Fixed width inference (for cases where the schema file is not available) is improved to prevent splitting inside
      standard data types.
    - Python translation now produces code that calls Pandas for supported CSV and fixed-width files.

- Extraction.Web
    - The NormalizeHtml method is now significantly simpler and more robust.
    - Now supports table constraints in which some cell examples are soft constraints (that is, they need not
      necessarily be satisfied but they help to converge to correct programs).  This can be useful in interactive
      settings where if the user provides new examples after a previous learning round, then any output of the previous
      learning round which the user has not changed can be treated as soft constraints.

- Transformation.Text
    - Learning performance improvements.
    - Improved readability of learned programs through constant folding.
    - Fixes to conditional program learning such that the correct program is learned and returned in more cases instead
      of the system indicating that it could not learn a program.  Also conditional patterns are better clustered
      together.

- Changes that only affect those building their own DSLs
    - The PROSE grammar specification language has been changed to only allow binding single variables in let
      expressions. None of our existing grammars used a let with multiple variables, and we decided to simplify the
      grammar handling logic by enforcing this as a constraint.
    - AST “holes” now have Ids and are equal if they have the same symbol and id.
    - There is a new subprogram translator extension point interface which enables pattern based code generators to be
      plugged into the overall translation system.

## Release 6.0.0 -- 2018/03/19

### Breaking Changes

- Our session base class no longer implements `IDisposable`, and its serialization format has changed because the 
  `AllowBackgroundComputations` member has been deleted.
  
- Session constraints and inputs are now maintained in smart collections rather than having custom Add/Remove methods.
    - For most consuming code the fix is just to replace calls to `session.AddConstraints` with
      `session.Constraints.Add` and `session.AddInputs` with `session.Inputs.Add` 
- The Python and Java translators now all take an OptimizeFor parameter which does NOT have a default value.  Callers
  should specify a value of OptimizeFor.Performance or OptimizeFor.Readability (where readability means that the program
  synthesized should be as easy as possible for humans to read and understand even if that means some reduction in the
  speed of execution for that program).
  
- Matching.Text no longer allows specifying negative examples or positive examples that are marked as hard constraints.
  Since the current implementation treats all examples as soft constraints, the API now makes that explicit.  Similarly,
  the `DisjunctionLimit` constraint is also always a soft constraint.
  
- Transformation.Text's `GetSignificantInputClustersAsync` method has been removed and replaced with
  `GetSignificantInputsAsync`.

### New Features

- Compound.Split
    - Now supports Multi-record splitting which enables splitting of files with key-value pairs and pivoting the results
      into a table with the keys as columns.

### Bug Fixes / Enhancements

- The `LearnTopK` method on `Session` has a new optional parameter for requesting not only the top K programs but also a
  random sample of additional programs learned.
  
- The dependency on the native Z3 library has been removed.

- Improvements to translation of programs.
    - Avoid lifting constants if translator is not opted for Performance.
    - Modify Python translator to not create classes for simple programs.
    - Perform Constant propagation, Copy propagation and Common subexpression optimization on translated programs
      (Java and Python).
    - Other readability improvements like aliasing in Python and shortening Python operator names.
    - Compound.Split now supports Python translations for simple delimiter and fixed width cases.  In an upcoming
      release all Compound.Split programs will support Python translation.
    - Specific to Transformation.Text
        - By default the generated program has a more natural function signature with an argument for each input column
          that is named appropriately rather than a taking a single dictionary of the inputs.
        - Programs produced use the more idiomatic + for concat and [:] for slice in appropriate places.
        - Dead-code elimination.
        - Function calls are not inlined but variables and literals are.
        - An extra variable is no longer created for the return value of a function.
- Extraction.Web
    - No longer escapes certain occurrences of hyphen in CSS selectors (when it occurs between two letters, a very
      common case) making them more readable.
    - Now supports entity-based extraction programs that include operators to extract data with respect to surrounding
      entities in the DOM context (e.g. extracting dates from bill receipts across different formats and providers).
    - A new previous program constraint which enables incremental table learning where a previously synthesized program
      can be supplied when synthesizing a new program which adds additional row/column selection information.  This can
      bring significant perf benefits for synthesizing programs to extract large tables.
    - Case insensitive text matching.
    - Possibly null values  are prevented in single column extractions.
    - Improved predicate learning to most specific and smallest selectors.
- Split.Text (and by extension Compound.Split)
    - Improvements to fixed width file detection including:
        - Better number data type recognition to include numbers preceded by “+/-“.
        - Reduced false positive left aligned column detection.
- Transformation.Text
    - Fixed a bug in datetime rounding learning where sometimes too many dates were rounded.

## Release 5.1.0 -- 2018/02/07

### Breaking Changes

- The packaging of PROSE functionality has been significantly refactored both to reduce the number of DLLs and
  dependencies and to allow fine-grained selection of the functionality to be included in a consuming application.
    - There is only one DLL per DSL plus one shared functionality DLL (Microsoft.ProgramSynthesis.Common.dll which
      replaces a variety of support DLLs used previously including Microsoft.ProgramSynthesis.dll,
      Microsoft.ProgramSynthesis.Utils.dll, Microsoft.ProgramSynthesis.Learning.dll and
      Microsoft.ProgramSynthesis.Wrangling.dll).
    - Each DSL is available in its own separate nuget package while the full SDK may still be referenced through the
      single package Microsoft.ProgramSynthesis which depends on all the other DSL nuget packages.
    - Removed dependencies on System.ValueTuple and System.Interactive.
- Tools for compling DSL grammars:
    - The tool `dslc.exe` has been renamed and turned into a dotnet CLI tool which may be executed with the command 
      `dotnet dslc`.
    - A pair of new nuget packages (Microsoft.ProgramSynthesis.Dslc and Microsoft.ProgramSynthesis.DslcTargets) now
      make it possible to compile a PROSE grammar in a new-style csproj file just by adding two lines to the csproj file
      and including the grammar file in the directory with the project.  This works with both .Net Core and .Net Desktop
      projects.  You can see this in action in our updated samples.  [This csproj, for instance.](
      https://github.com/Microsoft/prose/blob/master/ProgramSynthesis/ProseSample.Substrings/ProseSample.Substrings.csproj)
    - The #reference directive in the grammar has been removed—instead references should be passed as commandline
      arguments.
- For authors of custom DSLs:
    - RuleLearners now return Optional<ProgramSet> rather than ProgramSet.  This allows unambiguous handling of the
      difference between a rule learner not applying and it applying but returning a null or empty set of results.
- Extraction.Json:
    - Signature of programs is now `Program<string, ITable<string>>` (meaning output is just a flat table not a tree).
    - Other general cleanup/simplification of the API.
- The Split.File DSL has been removed and all of its capabilities have been merged into Compound.Split which now
  produces programs that will split a file into rows and then split each of those rows into columns.

- Transformation.Text:
    - IIndexableRow public interface: Previously methods operated on “object” types and casts were required to map to
      the actual type in use.  Now they accept strings directly (the only type currently in use) and we will add
      overloads for other types when supported in the future.  So all types can be supported without needing
      inefficient cast operations.
    - AutoComplete now uses IRow instead of IEnumerable<string> for input.

### New Features

- Extraction.Web is a new DSL for extracting structured data from HTML pages.
    - Can extract fields, sequences or tables given examples of specific web regions or text strings.
    - Integrates with Transformation.Text so the resulting extraction programs can also perform simple transformations
      on the data such as extracting substrings
    - Uses CSS selectors to perform extraction based on the full set of queues available in the document including
      formatting.
    - Has a concept of externally pluggable entity detectors which may be supplied by the consumer and can detect
      arbitrary entities in a text string (eg. an EntityDetecter might be written which detects instances of city
      names by consulting an external database).
- Translation of learned programs to Java so that they can be executed on the JVM has been added to several DSLs
  including:
    - Transformation.Text
    - Split.Text
    - Extraction.Json

### Bug Fixes / Enhancements

- Compound.Split:
    - Considers more lines when determining the column delimiter.
    - Examines header of file for additional clues to find delimiters.
    - Skips very sparse data rows (likely comment rows).
    - Now supports gathering telemetry through the `ILogger` interface.
- Conditionals:
    - DSL now has IsNull and IsWhiteSpace predicates which improve clustering of conditional program cases.
- Extraction.Json:
    - Supports streaming execution.
    - Can parse single line json documents with extra prefix and/or suffix characters.
- Matching.Text:
    - A new, greatly improved clustering algorithm.
    - Improved accurancy of reported fraction for each pattern (ie. the percentage of the data which that pattern
      matches).
      Previously it was inaccurate when duplicates were present.
    - Better regex generation.
    - Perf improvements.
- Split.Text:
    - Now supports gathering telemetry through the `ILogger` interface.
- Transformation.Json:
    - Automatic conversion of strings to objects and vice versa.
    - Better support for text transformation of json values.
    - Support for text transformation output from multiple json values (allowing merging of multiple values into a
      single string output value, etc.).
- Transformation.Text:
    - Avoids using the concat operator for programs learned from examples where the entire input appears in the
      output.
    - Bug fixed related to examples with explicit null output.
    - Performance improvements to learning times.
    - A simpler API for entity extraction from a column profile (not just through the full derived column mechanism).
    - Supports transforming dates into the week of the year, and this is preferred to week of month when the examples
      are ambiguous.
- Transformation.Tree:
    - Bug is fixed in sequence node synthesis.
    - Previously could not learn an Order By transformation when there isn't an alias.
- Concurrency:
    - It is now possible to execute two calls to synthesize programs on different threads in parallel.

- The `LearnTopK` method now takes an optional `IFeature` parameter which may be used to rank programs using a different
  feature than the default ranking score.

- Many other general performance and stability fixes.

## Release 4.0.0 -- 2017/09/15

### Breaking Changes

- State.Create method has been split into two versions: CreateForLearning and CreateForExecution.  The CreateForLearning
  version can be slower but is necessary (as you might imagine from the name) when the state is going to be used for
  learning programs as opposed to just executing programs that were previously learned.
- Moved CoreClr to .netstandard 2.0--as part of this change upgraded some dependencies:
    - System.ValueTuple 4.4.0 (up from 4.3.1)
    - Newtonsoft.Json 10.03 (up from 8.0.2)
    - Plus the move to .netstandard 2.0 and corresponding upgrade to related corefx packages (mostly moving to version
      4.4.0)

### New Features

- A new API has been added for working with significant inputs which enables quick retrieval of some significant inputs
  and then async calculation and later retrieval of additional significant inputs as they become available.
- Matching.Text now exposes the DescriptionTokens property to enable rich-text rendering of pattern descriptions.

### Bug fixes / Enhancements

- Our nuget package should now work properly in both desktop .net and net core projects.
- Compound.Split has a new constraint for specifying column delimiters.
- Transformation.Text now supports the ISO week number format (eg. date is in week #32 of the year).
- Better handline of empty json strings.
- Robustness improvements for Split.Text--better handle input that is json with mixed delimiters as well as redundant
  examples.
- Miscellaneous perf and correctness fixes

## Release 3.2.0 -- 2017/08/16

### New Features

- A new Transformation.Tree DSL which may be used in scenarios such as code transformation/refactoring.
- Transformation.Text improvements to date/time and number handling:
    - European date/time and number formats
    - Day of meek in month support (like 3rd monday in April, but note that specifying numbers as
      ordinals like 3rd instead of 3 is not yet supported)
    - Lowercase am/pm in times
- Matching.Text now has the ability to generate representative examples and a regex description for each cluster.

### Bug fixes / Enhancements

- New Compound.Split streaming interface for running split programs on large files and the ability to specify a fill
  strategy for filling values in non-rectangular tables.
- Fixes for advanced scenarios related to creating new DSLs:
    - A fix for a long-standing bug related to learning cache lookups in recursive grammars.
    - A two-pass mode for dslc which allows strongly-typed program-fragment builders to be used in all code.
- Extraction.Json no longer treats bare strings/numbers as valid json, so it won't learn a no-op program for them.
- Miscellaneous correctness and performance improvements.

## Release 3.1.3 -- 2017/07/18

### Bug fixes / Enhancements

- Transformation.Text date/time support has been fixed to prefer ranges over rounding in some key cases.
- A number of general stability and performance improvements.

## Release 3.0.0 -- 2017/06/28

*This release fixes the issues using the nuget packages in VS2015 and VS2017 (when using old-style packages.config).*

### Breaking Changes

- De-serializing programs in human readable format is removed.  Human readable was never a reliable serialization format
  (although it is nice for debugging purposes) because it does not contain enough information to guarantee backward
  compatibility. We have removed de-serialization support to encourage the use of the XML serialization format.  This
  also means that the ANTLR runtime dependency has been removed from our core nuget package.
- The paraphrasing library is removed.  Transformation.Text still contains its separate support for the explanations
  feature. In effect this is an implementation detail, but consumers may need to remove any DLL references they had to
  Microsoft.ProgramSynthesis.Paraphrasing.
- Moved Microsoft.ProgramSynthesis.Compiler.dll from the main nuget package to the compiler package.  Previously the
  compiler package just contained the dslc.exe tool for compiling a grammar into source code so that it can be built
  into a DSL's DLL, now it also contains the DLL which is used for runtime parsing of grammar files.  This means that
  the core package which is all you need if you are consuming prebuilt DSLs no longer has a dependency on ANTLR4.Runtime
  (but the compiler package does have that dependency).
- The netstandard1.6 libraries are now built for CoreClr 1.1.
- The SDK now depends on System.Collections.Immutable version 1.3.0 (up from 1.2.0) and NewtonSoft.Json version 8.0.3
  (up from 8.0.2).
- All uses of Tuple have been replaced with ValueTuple.
- Extraction.Json:
    - No longer automatically treats arrays as objects.  Instead clients are expected to use constraints to control how
      arrays are flattened.  Default is for arrays to turn into rows, but there is a new constraint which allows
      flattening them into columns.

### Bug fixes / Enhancements

- Detection.DataType is a new DLL added to the package which when given a series of strings can detect the datatypes
  those string values represent (ie. number, date, etc.).
- Extraction.Json:
    - Fixed case where a single-line JSON was misidentified as NDJSON.
- Transformation.Text:
    - Rounding times.
    - Rounding of scaled numbers.
    - DayOfYear (1-366) format for dates.
    - Performance improvements.
    - Stability fixes.
- Split.Text
    - Field detection, expressiveness and error handling improvements.
    - Performance improvements (especially for large string sizes).
- Grammar files now support an annotation to indicate that a rule is deprecated (but kept in the grammar to allow
  deserialization of programs learned on older versions).

## Release 2.3.0 -- 2017/05/15

*Note: We have had some reports of folks having trouble using the public nuget packages in VS2015 since the 2.0.0
release. We are aware of the issues and hope to have a fix soon.  In the meantime, the available packages should work in
VS2017.*

### Bug fixes / Enhancements

- This release includes significant performance improvements including:
    - A long-standing memory leak was fixed in the core framework that affected learning performance.
    - Runtime performance improvements for generated Python programs (on order of 2x faster).
    - Transformation.Text learning performance is improved.      
    - Transformation.Text significant inputs performance is improved.
    - Transformation.Text date/time parsing (both during learning and dat runtime) performance is improved.
- Fixed bugs in Split.Text related to inconsistent number of occurrences of delimiters (e.g. space delimiter in phrases
  of different lengths).
- When a delimiter is specified, Split.Text now ensures that the dominant format selected contains at least one
  delimiter occurrence.
- Extraction.Json programs now contain metadata information indicating if they extract an object, an array or an object
  which has only a single array property.
- Fix for a bug when generating programs for MergeColumns constraints with no separators/constants specified if there
  was a constant string at the end.

## Release 2.2.0 -- 2017/04/24

### Bug fixes / Enhancements

- Transformation.Text now supports scientific notation and more flexible ways of indicating that a number is negative
  when parsing.  (It does not format numbers in these ways--only parses them.)
- Transformation.Text's significant inputs support has been improved in cases where no program can be learned from the
  current set of examples.
- Some API usability improvements have been made to Matching.Text.
- Miscellaneous performance and stability improvements.

## Release 2.1.0 -- 2017/04/17

### New Features

- Split.Text now supports fixed width files.
- Transformation.Json now includes Transformation.Text support.  This means it can synthesize programs which not only
  change the structure of a json document but also transform the values.

### Bug fixes / Enhancements

- A number of bug fixes/enhancements were made to Extraction.Json--especially for the scenario of handling
  new-line delimited json (ndjson) documents or the similar case of having an input column containing a json
  document in each row which you want to extract into multiple output columns.  These changes include:
    - Supporting empty rows in ndjson documents.
    - Handling json files with byte order marks (BOMs) at the beginning.
    - Allowing different sets of properties and/or the properties appearing in different order when extracting
      from a series of json documents.
    - Supporting a `NamePrefix` constraint so that output column names can all be given a common prefix.
- Tranformation.Text now accepts strongly typed number and date inputs in addition to strings improving both
  performance and correctness for those cases.
- Miscellaneous Transformation.Text date handling improvements (both performance and correctness)
- Extraction.Json now supports JSON arrays that have only values -- eg. `[ "1", "2" ]`
- Compound.Split API simplification: The InputStream constraint is no longer used to specify that the input comes
  from a stream.  Instead, if a stream is passed to the session, it assumes that behavior automatically.
- Split.File now supports new lines in quotes.

## Release 2.0.1 -- 2017/03/17

Minor bug fix release.

## Release 2.0.0 -- 2017/03/16

We have bumped the major number this time around because this release includes a breaking change (and we are doing our
best to conform to semantic versioning).  The change is to the way `dslc` compiles grammar files.  Previously it
produced a .Net assembly.  Now it outputs c# source code which can be compiled into your main DSL assembly.  This not
only reduces the number of assemblies required to deploy your solution but also allows us to generate helper methods for
advanced scenarios involving manually creating program trees for a DSL.

### New Features

- Grammar files may now have a `using grammar <grammarName> = <class>.<property>` statement to indicate that the grammar
  depends on another grammar.
- Extraction.Json now supports learning programs from multiple input json documents.  This makes it possible to have a
  scenario like Split.Text where a column of data contains a different json document on each row, and you want to
  flatten all of those json documents into a set of new columns extracted from the json.
- Telemetry support.  Users of our DSLs may now pass an implementation of our `ILogger` interface to the `Session`
  object for the DSL.  If this is done, PROSE will call the `ILogger` with telemetry information such as the time
  required to learn programs, etc.

### Bug fixes / Enhancements

- Significant inputs are now computed using the Z3 theorem prover from MSR (included in our nuget package as a set of 
  native libraries for Windows, Mac and Linux) which significantly decreases the time required to determine them.
- Transformation.Text significant inputs now include ambiguous dates.
- Extraction.Json now supports extra characters at the end of lines when extracting from new-line delimited json docs.
- Split.Text now supports contexttual field-based delimiters which improve learning performance and address multiple
  bugs.
- Translation capabilities have now been merged directly into their main DSL assemblies as part of our long-term effort
  to reduce the number of assemblies per DSL.
- Matching.Text now uses an improved sampling algorithm for clustering.
- Several other ranking and stability improvements.


## Release 1.1.0 -- 2017/02/15

With this release we are starting a regular monthly public release rhythm.  The biggest change in this month's release
is major improvements to our samples and documentation.  At the same time we have added several small new features and
bug fixes.

### New Features

- Made more spec methods `protected internal` to enable third-party implementation of `Spec` subclasses.
- Added new documentation and samples to facilitate third-party DSL development. Fixes
  [\#10](https://github.com/Microsoft/prose/issues/10).
- More flexibility in time ranges in `Transformation.Text`.
- Allowed omitting leading zeros at the start of numeric date formats in `Transformation.Text`.

### Bug Fixes

- Improved `RunMerge`'s handling of empty lines in `Split.File`.
- Fixed learning with missing lookahead/lookbehind regexes in `Extraction.Text`
  ([\#7](https://github.com/Microsoft/prose/issues/7)).
- Improved `Extraction.Json`'s handling of documents where the top-level is an array or a single object containing an
  array.
- Several bug fixes that improve stability, performance and reduce the number of examples required to learn the intended
  program across the SDK.


## Release 1.0.3 -- 2017/01/22

First public release. Added support for .NET Core as well as several new DSLs.

## Release 0.1.1 -- 2015/10/29

First public preview.
