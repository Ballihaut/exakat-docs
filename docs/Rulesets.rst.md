Rulesets {#Rulesets}
========

Presentation
------------

Analysis are grouped in different rulesets, that may be run
independantly. Each ruleset has a focus target,

Rulesets runs all its analysis and any needed dependency.

Rulesets are configured with the -T option, when running exakat in
command line. For example :

    php exakat.phar analyze -p <project> -T <Security>

List of rulesets
----------------

Here is the list of the current rulesets supported by Exakat Engine.

  ------------------------------------------------------------- ------------------------------------------------
  Name                                                          Description

  `Analyze`{.interpreted-text role="ref"}                       Check for common best practices.

  `CI-checks`{.interpreted-text role="ref"}                     Quick check for common best practices.

  `Dead code <dead-code>`{.interpreted-text role="ref"}         Check the unused code or unreachable code.

  `Suggestions`{.interpreted-text role="ref"}                   List of possible modernisation of the PHP code.

  `CompatibilityPHP74`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                7.4. It is known as php-src, work in progress.

  `CompatibilityPHP73`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                7.3.

  `CompatibilityPHP72`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                7.2.

  `CompatibilityPHP71`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                7.1.

  `CompatibilityPHP80`{.interpreted-text role="ref"}            Work in progress. The first rules are in, but
                                                                far from finished

  `Performances`{.interpreted-text role="ref"}                  Check the code for slow code.

  `Security`{.interpreted-text role="ref"}                      Check the code for common security bad
                                                                practices, especially in the Web environnement.

  `Top10`{.interpreted-text role="ref"}                         The most common issues found in the code

  `Classreview`{.interpreted-text role="ref"}                   A set of rules dedicate to class hygiene

  `LintButWontExec`{.interpreted-text role="ref"}               Check the code for common errors that will lead
                                                                to a Fatal error on production, but lint fine.

  `CompatibilityPHP70`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                7.0.

  `CompatibilityPHP56`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                5.6.

  `CompatibilityPHP55`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                5.5.

  `CompatibilityPHP54`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                5.4.

  `CompatibilityPHP53`{.interpreted-text role="ref"}            List features that are incompatible with PHP
                                                                5.3.

  `Coding Conventions <coding-conventions>`{.interpreted-text   List coding conventions violations.
  role="ref"}                                                   

  `Semantics`{.interpreted-text role="ref"}                     Checks the meanings found the names of the code.

  `Typechecks`{.interpreted-text role="ref"}                    Checks related to types.

  `Rector`{.interpreted-text role="ref"}                        Suggests configuration to apply changes with
                                                                Rector

  `php-cs-fixable`{.interpreted-text role="ref"}                Suggests configuration to apply changes with
                                                                PHP-CS-FIXER
  ------------------------------------------------------------- ------------------------------------------------

Note : in command line, don\'t forget to add quotes to rulesets\' names
that include white space.

Rulesets details
----------------

### Analyze

This ruleset centralizes a large number of classic trap and pitfalls
when writing PHP.

Total : 415 analysis

-   `$this Belongs To Classes Or Traits <$this-belongs-to-classes-or-traits>`{.interpreted-text
    role="ref"}
-   `$this Is Not An Array <$this-is-not-an-array>`{.interpreted-text
    role="ref"}
-   `$this Is Not For Static Methods <$this-is-not-for-static-methods>`{.interpreted-text
    role="ref"}
-   `@ Operator <@-operator>`{.interpreted-text role="ref"}
-   `Abstract Or Implements <abstract-or-implements>`{.interpreted-text
    role="ref"}
-   `Abstract Static Methods <abstract-static-methods>`{.interpreted-text
    role="ref"}
-   `Access Protected Structures <access-protected-structures>`{.interpreted-text
    role="ref"}
-   `Accessing Private <accessing-private>`{.interpreted-text
    role="ref"}
-   `Adding Zero <adding-zero>`{.interpreted-text role="ref"}
-   `Aliases Usage <aliases-usage>`{.interpreted-text role="ref"}
-   `Already Parents Interface <already-parents-interface>`{.interpreted-text
    role="ref"}
-   `Already Parents Trait <already-parents-trait>`{.interpreted-text
    role="ref"}
-   `Altering Foreach Without Reference <altering-foreach-without-reference>`{.interpreted-text
    role="ref"}
-   `Alternative Syntax Consistence <alternative-syntax-consistence>`{.interpreted-text
    role="ref"}
-   `Always Positive Comparison <always-positive-comparison>`{.interpreted-text
    role="ref"}
-   `Ambiguous Array Index <ambiguous-array-index>`{.interpreted-text
    role="ref"}
-   `Ambiguous Static <ambiguous-static>`{.interpreted-text role="ref"}
-   `Ambiguous Visibilities <ambiguous-visibilities>`{.interpreted-text
    role="ref"}
-   `Array_Fill() With Objects <array\_fill()-with-objects>`{.interpreted-text
    role="ref"}
-   `Array_merge Needs Array Of Arrays <array\_merge-needs-array-of-arrays>`{.interpreted-text
    role="ref"}
-   `Assert Function Is Reserved <assert-function-is-reserved>`{.interpreted-text
    role="ref"}
-   `Assign And Compare <assign-and-compare>`{.interpreted-text
    role="ref"}
-   `Assign Default To Properties <assign-default-to-properties>`{.interpreted-text
    role="ref"}
-   `Assign With And Precedence <assign-with-and-precedence>`{.interpreted-text
    role="ref"}
-   `Assigned Twice <assigned-twice>`{.interpreted-text role="ref"}
-   `Assumptions <assumptions>`{.interpreted-text role="ref"}
-   `Avoid Optional Properties <avoid-optional-properties>`{.interpreted-text
    role="ref"}
-   `Avoid Parenthesis <avoid-parenthesis>`{.interpreted-text
    role="ref"}
-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Avoid Using stdClass <avoid-using-stdclass>`{.interpreted-text
    role="ref"}
-   `Avoid get_class() <avoid-get\_class()>`{.interpreted-text
    role="ref"}
-   `Avoid mb_dectect_encoding() <avoid-mb\_dectect\_encoding()>`{.interpreted-text
    role="ref"}
-   `Avoid option arrays in constructors <avoid-option-arrays-in-constructors>`{.interpreted-text
    role="ref"}
-   `Bad Constants Names <bad-constants-names>`{.interpreted-text
    role="ref"}
-   `Bail Out Early <bail-out-early>`{.interpreted-text role="ref"}
-   `Break Outside Loop <break-outside-loop>`{.interpreted-text
    role="ref"}
-   `Buried Assignation <buried-assignation>`{.interpreted-text
    role="ref"}
-   `Callback Function Needs Return <callback-function-needs-return>`{.interpreted-text
    role="ref"}
-   `Can't Extend Final <can't-extend-final>`{.interpreted-text
    role="ref"}
-   `Can't Throw Throwable <can't-throw-throwable>`{.interpreted-text
    role="ref"}
-   `Cancelled Parameter <cancelled-parameter>`{.interpreted-text
    role="ref"}
-   `Cant Implement Traversable <cant-implement-traversable>`{.interpreted-text
    role="ref"}
-   `Cant Instantiate Class <cant-instantiate-class>`{.interpreted-text
    role="ref"}
-   `Cast To Boolean <cast-to-boolean>`{.interpreted-text role="ref"}
-   `Casting Ternary <casting-ternary>`{.interpreted-text role="ref"}
-   `Catch Overwrite Variable <catch-overwrite-variable>`{.interpreted-text
    role="ref"}
-   `Catch Undefined Variable <catch-undefined-variable>`{.interpreted-text
    role="ref"}
-   `Check All Types <check-all-types>`{.interpreted-text role="ref"}
-   `Check JSON <check-json>`{.interpreted-text role="ref"}
-   `Check On __Call Usage <check-on-\_\_call-usage>`{.interpreted-text
    role="ref"}
-   `Class Could Be Final <class-could-be-final>`{.interpreted-text
    role="ref"}
-   `Class Should Be Final By Ocramius <class-should-be-final-by-ocramius>`{.interpreted-text
    role="ref"}
-   `Class Without Parent <class-without-parent>`{.interpreted-text
    role="ref"}
-   `Class, Interface Or Trait With Identical Names <class,-interface-or-trait-with-identical-names>`{.interpreted-text
    role="ref"}
-   `Clone With Non-Object <clone-with-non-object>`{.interpreted-text
    role="ref"}
-   `Coalesce And Concat <coalesce-and-concat>`{.interpreted-text
    role="ref"}
-   `Common Alternatives <common-alternatives>`{.interpreted-text
    role="ref"}
-   `Compared Comparison <compared-comparison>`{.interpreted-text
    role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Concat Empty String <concat-empty-string>`{.interpreted-text
    role="ref"}
-   `Concrete Visibility <concrete-visibility>`{.interpreted-text
    role="ref"}
-   `Constant Class <constant-class>`{.interpreted-text role="ref"}
-   `Constant Comparison <constant-comparison>`{.interpreted-text
    role="ref"}
-   `Constant Typo Looks Like A Variable <constant-typo-looks-like-a-variable>`{.interpreted-text
    role="ref"}
-   `Constants Created Outside Its Namespace <constants-created-outside-its-namespace>`{.interpreted-text
    role="ref"}
-   `Constants With Strange Names <constants-with-strange-names>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Could Be Abstract Class <could-be-abstract-class>`{.interpreted-text
    role="ref"}
-   `Could Be Else <could-be-else>`{.interpreted-text role="ref"}
-   `Could Be Static <could-be-static>`{.interpreted-text role="ref"}
-   `Could Be Stringable <could-be-stringable>`{.interpreted-text
    role="ref"}
-   `Could Make A Function <could-make-a-function>`{.interpreted-text
    role="ref"}
-   `Could Use Short Assignation <could-use-short-assignation>`{.interpreted-text
    role="ref"}
-   `Could Use __DIR__ <could-use-\_\_dir\_\_>`{.interpreted-text
    role="ref"}
-   `Could Use self <could-use-self>`{.interpreted-text role="ref"}
-   `Could Use str_repeat() <could-use-str\_repeat()>`{.interpreted-text
    role="ref"}
-   `Crc32() Might Be Negative <crc32()-might-be-negative>`{.interpreted-text
    role="ref"}
-   `Cyclic References <cyclic-references>`{.interpreted-text
    role="ref"}
-   `Dangling Array References <dangling-array-references>`{.interpreted-text
    role="ref"}
-   `Deep Definitions <deep-definitions>`{.interpreted-text role="ref"}
-   `Dependant Abstract Classes <dependant-abstract-classes>`{.interpreted-text
    role="ref"}
-   `Dependant Trait <dependant-trait>`{.interpreted-text role="ref"}
-   `Deprecated PHP Functions <deprecated-php-functions>`{.interpreted-text
    role="ref"}
-   `Different Argument Counts <different-argument-counts>`{.interpreted-text
    role="ref"}
-   `Don't Change Incomings <don't-change-incomings>`{.interpreted-text
    role="ref"}
-   `Don't Echo Error <don't-echo-error>`{.interpreted-text role="ref"}
-   `Don't Pollute Global Space <don't-pollute-global-space>`{.interpreted-text
    role="ref"}
-   `Don't Read And Write In One Expression <don't-read-and-write-in-one-expression>`{.interpreted-text
    role="ref"}
-   `Don't Send $this In Constructor <don't-send-$this-in-constructor>`{.interpreted-text
    role="ref"}
-   `Don't Unset Properties <don't-unset-properties>`{.interpreted-text
    role="ref"}
-   `Dont Change The Blind Var <dont-change-the-blind-var>`{.interpreted-text
    role="ref"}
-   `Dont Collect Void <dont-collect-void>`{.interpreted-text
    role="ref"}
-   `Dont Mix ++ <dont-mix-++>`{.interpreted-text role="ref"}
-   `Double Assignation <double-assignation>`{.interpreted-text
    role="ref"}
-   `Double Instructions <double-instructions>`{.interpreted-text
    role="ref"}
-   `Double Object Assignation <double-object-assignation>`{.interpreted-text
    role="ref"}
-   `Drop Else After Return <drop-else-after-return>`{.interpreted-text
    role="ref"}
-   `Echo With Concat <echo-with-concat>`{.interpreted-text role="ref"}
-   `Else If Versus Elseif <else-if-versus-elseif>`{.interpreted-text
    role="ref"}
-   `Empty Blocks <empty-blocks>`{.interpreted-text role="ref"}
-   `Empty Classes <empty-classes>`{.interpreted-text role="ref"}
-   `Empty Function <empty-function>`{.interpreted-text role="ref"}
-   `Empty Instructions <empty-instructions>`{.interpreted-text
    role="ref"}
-   `Empty Interfaces <empty-interfaces>`{.interpreted-text role="ref"}
-   `Empty List <empty-list>`{.interpreted-text role="ref"}
-   `Empty Namespace <empty-namespace>`{.interpreted-text role="ref"}
-   `Empty Traits <empty-traits>`{.interpreted-text role="ref"}
-   `Empty Try Catch <empty-try-catch>`{.interpreted-text role="ref"}
-   `Eval() Usage <eval()-usage>`{.interpreted-text role="ref"}
-   `Exit() Usage <exit()-usage>`{.interpreted-text role="ref"}
-   `Failed Substr Comparison <failed-substr-comparison>`{.interpreted-text
    role="ref"}
-   `Fn Argument Variable Confusion <fn-argument-variable-confusion>`{.interpreted-text
    role="ref"}
-   `Foreach On Object <foreach-on-object>`{.interpreted-text
    role="ref"}
-   `Foreach Reference Is Not Modified <foreach-reference-is-not-modified>`{.interpreted-text
    role="ref"}
-   `Forgotten Interface <forgotten-interface>`{.interpreted-text
    role="ref"}
-   `Forgotten Thrown <forgotten-thrown>`{.interpreted-text role="ref"}
-   `Forgotten Visibility <forgotten-visibility>`{.interpreted-text
    role="ref"}
-   `Forgotten Whitespace <forgotten-whitespace>`{.interpreted-text
    role="ref"}
-   `Fully Qualified Constants <fully-qualified-constants>`{.interpreted-text
    role="ref"}
-   `Global Usage <global-usage>`{.interpreted-text role="ref"}
-   `Hardcoded Passwords <hardcoded-passwords>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms <hash-algorithms>`{.interpreted-text role="ref"}
-   `Hidden Nullable <hidden-nullable>`{.interpreted-text role="ref"}
-   `Hidden Use Expression <hidden-use-expression>`{.interpreted-text
    role="ref"}
-   `Htmlentities Calls <htmlentities-calls>`{.interpreted-text
    role="ref"}
-   `Identical Conditions <identical-conditions>`{.interpreted-text
    role="ref"}
-   `Identical Consecutive Expression <identical-consecutive-expression>`{.interpreted-text
    role="ref"}
-   `Identical On Both Sides <identical-on-both-sides>`{.interpreted-text
    role="ref"}
-   `If With Same Conditions <if-with-same-conditions>`{.interpreted-text
    role="ref"}
-   `Iffectations <iffectations>`{.interpreted-text role="ref"}
-   `Illegal Name For Method <illegal-name-for-method>`{.interpreted-text
    role="ref"}
-   `Implement Is For Interface <implement-is-for-interface>`{.interpreted-text
    role="ref"}
-   `Implemented Methods Are Public <implemented-methods-are-public>`{.interpreted-text
    role="ref"}
-   `Implied If <implied-if>`{.interpreted-text role="ref"}
-   `Implode() Arguments Order <implode()-arguments-order>`{.interpreted-text
    role="ref"}
-   `Inclusion Wrong Case <inclusion-wrong-case>`{.interpreted-text
    role="ref"}
-   `Incompatible Signature Methods <incompatible-signature-methods>`{.interpreted-text
    role="ref"}
-   `Incompatible Signature Methods With Covariance <incompatible-signature-methods-with-covariance>`{.interpreted-text
    role="ref"}
-   `Incompilable Files <incompilable-files>`{.interpreted-text
    role="ref"}
-   `Inconsistent Elseif <inconsistent-elseif>`{.interpreted-text
    role="ref"}
-   `Indices Are Int Or String <indices-are-int-or-string>`{.interpreted-text
    role="ref"}
-   `Infinite Recursion <infinite-recursion>`{.interpreted-text
    role="ref"}
-   `Instantiating Abstract Class <instantiating-abstract-class>`{.interpreted-text
    role="ref"}
-   `Insufficient Typehint <insufficient-typehint>`{.interpreted-text
    role="ref"}
-   `Interfaces Don't Ensure Properties <interfaces-don't-ensure-properties>`{.interpreted-text
    role="ref"}
-   `Interfaces Is Not Implemented <interfaces-is-not-implemented>`{.interpreted-text
    role="ref"}
-   `Invalid Constant Name <invalid-constant-name>`{.interpreted-text
    role="ref"}
-   `Invalid Pack Format <invalid-pack-format>`{.interpreted-text
    role="ref"}
-   `Invalid Regex <invalid-regex>`{.interpreted-text role="ref"}
-   `Is Actually Zero <is-actually-zero>`{.interpreted-text role="ref"}
-   `Is_A() With String <is\_a()-with-string>`{.interpreted-text
    role="ref"}
-   `Logical Mistakes <logical-mistakes>`{.interpreted-text role="ref"}
-   `Logical Should Use Symbolic Operators <logical-should-use-symbolic-operators>`{.interpreted-text
    role="ref"}
-   `Logical To in_array <logical-to-in\_array>`{.interpreted-text
    role="ref"}
-   `Lone Blocks <lone-blocks>`{.interpreted-text role="ref"}
-   `Long Arguments <long-arguments>`{.interpreted-text role="ref"}
-   `Lost References <lost-references>`{.interpreted-text role="ref"}
-   `Make Global A Property <make-global-a-property>`{.interpreted-text
    role="ref"}
-   `Max Level Of Nesting <max-level-of-nesting>`{.interpreted-text
    role="ref"}
-   `Maybe Missing New <maybe-missing-new>`{.interpreted-text
    role="ref"}
-   `Mbstring Third Arg <mbstring-third-arg>`{.interpreted-text
    role="ref"}
-   `Mbstring Unknown Encoding <mbstring-unknown-encoding>`{.interpreted-text
    role="ref"}
-   `Memoize MagicCall <memoize-magiccall>`{.interpreted-text
    role="ref"}
-   `Merge If Then <merge-if-then>`{.interpreted-text role="ref"}
-   `Method Collision Traits <method-collision-traits>`{.interpreted-text
    role="ref"}
-   `Method Could Be Static <method-could-be-static>`{.interpreted-text
    role="ref"}
-   `Method Signature Must Be Compatible <method-signature-must-be-compatible>`{.interpreted-text
    role="ref"}
-   `Methods Without Return <methods-without-return>`{.interpreted-text
    role="ref"}
-   `Mismatch Parameter And Type <mismatch-parameter-and-type>`{.interpreted-text
    role="ref"}
-   `Mismatch Parameter Name <mismatch-parameter-name>`{.interpreted-text
    role="ref"}
-   `Mismatch Properties Typehints <mismatch-properties-typehints>`{.interpreted-text
    role="ref"}
-   `Mismatch Type And Default <mismatch-type-and-default>`{.interpreted-text
    role="ref"}
-   `Mismatched Default Arguments <mismatched-default-arguments>`{.interpreted-text
    role="ref"}
-   `Mismatched Ternary Alternatives <mismatched-ternary-alternatives>`{.interpreted-text
    role="ref"}
-   `Mismatched Typehint <mismatched-typehint>`{.interpreted-text
    role="ref"}
-   `Missing Abstract Method <missing-abstract-method>`{.interpreted-text
    role="ref"}
-   `Missing Cases In Switch <missing-cases-in-switch>`{.interpreted-text
    role="ref"}
-   `Missing Include <missing-include>`{.interpreted-text role="ref"}
-   `Missing Parenthesis <missing-parenthesis>`{.interpreted-text
    role="ref"}
-   `Missing Some Returntype <missing-some-returntype>`{.interpreted-text
    role="ref"}
-   `Mixed Concat And Interpolation <mixed-concat-and-interpolation>`{.interpreted-text
    role="ref"}
-   `Modernize Empty With Expression <modernize-empty-with-expression>`{.interpreted-text
    role="ref"}
-   `Modified Typed Parameter <modified-typed-parameter>`{.interpreted-text
    role="ref"}
-   `Multiple Alias Definitions <multiple-alias-definitions>`{.interpreted-text
    role="ref"}
-   `Multiple Alias Definitions Per File <multiple-alias-definitions-per-file>`{.interpreted-text
    role="ref"}
-   `Multiple Class Declarations <multiple-class-declarations>`{.interpreted-text
    role="ref"}
-   `Multiple Constant Definition <multiple-constant-definition>`{.interpreted-text
    role="ref"}
-   `Multiple Declaration Of Strict_types <multiple-declaration-of-strict\_types>`{.interpreted-text
    role="ref"}
-   `Multiple Identical Trait Or Interface <multiple-identical-trait-or-interface>`{.interpreted-text
    role="ref"}
-   `Multiple Index Definition <multiple-index-definition>`{.interpreted-text
    role="ref"}
-   `Multiple Type Variable <multiple-type-variable>`{.interpreted-text
    role="ref"}
-   `Multiples Identical Case <multiples-identical-case>`{.interpreted-text
    role="ref"}
-   `Multiply By One <multiply-by-one>`{.interpreted-text role="ref"}
-   `Must Call Parent Constructor <must-call-parent-constructor>`{.interpreted-text
    role="ref"}
-   `Must Return Methods <must-return-methods>`{.interpreted-text
    role="ref"}
-   `Negative Power <negative-power>`{.interpreted-text role="ref"}
-   `Nested Ifthen <nested-ifthen>`{.interpreted-text role="ref"}
-   `Nested Ternary <nested-ternary>`{.interpreted-text role="ref"}
-   `Never Used Parameter <never-used-parameter>`{.interpreted-text
    role="ref"}
-   `Never Used Properties <never-used-properties>`{.interpreted-text
    role="ref"}
-   `Next Month Trap <next-month-trap>`{.interpreted-text role="ref"}
-   `No Append On Source <no-append-on-source>`{.interpreted-text
    role="ref"}
-   `No Boolean As Default <no-boolean-as-default>`{.interpreted-text
    role="ref"}
-   `No Choice <no-choice>`{.interpreted-text role="ref"}
-   `No Class In Global <no-class-in-global>`{.interpreted-text
    role="ref"}
-   `No Direct Call To Magic Method <no-direct-call-to-magic-method>`{.interpreted-text
    role="ref"}
-   `No Direct Usage <no-direct-usage>`{.interpreted-text role="ref"}
-   `No Empty Regex <no-empty-regex>`{.interpreted-text role="ref"}
-   `No Hardcoded Hash <no-hardcoded-hash>`{.interpreted-text
    role="ref"}
-   `No Hardcoded Ip <no-hardcoded-ip>`{.interpreted-text role="ref"}
-   `No Hardcoded Path <no-hardcoded-path>`{.interpreted-text
    role="ref"}
-   `No Hardcoded Port <no-hardcoded-port>`{.interpreted-text
    role="ref"}
-   `No Literal For Reference <no-literal-for-reference>`{.interpreted-text
    role="ref"}
-   `No Magic Method With Array <no-magic-method-with-array>`{.interpreted-text
    role="ref"}
-   `No Need For Else <no-need-for-else>`{.interpreted-text role="ref"}
-   `No Need For Triple Equal <no-need-for-triple-equal>`{.interpreted-text
    role="ref"}
-   `No Parenthesis For Language Construct <no-parenthesis-for-language-construct>`{.interpreted-text
    role="ref"}
-   `No Public Access <no-public-access>`{.interpreted-text role="ref"}
-   `No Real Comparison <no-real-comparison>`{.interpreted-text
    role="ref"}
-   `No Reference For Ternary <no-reference-for-ternary>`{.interpreted-text
    role="ref"}
-   `No Reference On Left Side <no-reference-on-left-side>`{.interpreted-text
    role="ref"}
-   `No Return Used <no-return-used>`{.interpreted-text role="ref"}
-   `No Self Referencing Constant <no-self-referencing-constant>`{.interpreted-text
    role="ref"}
-   `No Spread For Hash <no-spread-for-hash>`{.interpreted-text
    role="ref"}
-   `No array_merge() In Loops <no-array\_merge()-in-loops>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `No isset() With empty() <no-isset()-with-empty()>`{.interpreted-text
    role="ref"}
-   `Non Ascii Variables <non-ascii-variables>`{.interpreted-text
    role="ref"}
-   `Non Nullable Getters <non-nullable-getters>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Non-constant Index In Array <non-constant-index-in-array>`{.interpreted-text
    role="ref"}
-   `Not Equal Is Not !== <not-equal-is-not-!==>`{.interpreted-text
    role="ref"}
-   `Not Not <not-not>`{.interpreted-text role="ref"}
-   `Null Or Boolean Arrays <null-or-boolean-arrays>`{.interpreted-text
    role="ref"}
-   `Objects Don't Need References <objects-don't-need-references>`{.interpreted-text
    role="ref"}
-   `Old Style Constructor <old-style-constructor>`{.interpreted-text
    role="ref"}
-   `Old Style __autoload() <old-style-\_\_autoload()>`{.interpreted-text
    role="ref"}
-   `One Variable String <one-variable-string>`{.interpreted-text
    role="ref"}
-   `Only Variable For Reference <only-variable-for-reference>`{.interpreted-text
    role="ref"}
-   `Only Variable Passed By Reference <only-variable-passed-by-reference>`{.interpreted-text
    role="ref"}
-   `Only Variable Returned By Reference <only-variable-returned-by-reference>`{.interpreted-text
    role="ref"}
-   `Or Die <or-die>`{.interpreted-text role="ref"}
-   `Overwritten Exceptions <overwritten-exceptions>`{.interpreted-text
    role="ref"}
-   `Overwritten Literals <overwritten-literals>`{.interpreted-text
    role="ref"}
-   `Overwritten Source And Value <overwritten-source-and-value>`{.interpreted-text
    role="ref"}
-   `PHP Keywords As Names <php-keywords-as-names>`{.interpreted-text
    role="ref"}
-   `Parent First <parent-first>`{.interpreted-text role="ref"}
-   `Parent, Static Or Self Outside Class <parent,-static-or-self-outside-class>`{.interpreted-text
    role="ref"}
-   `Pathinfo() Returns May Vary <pathinfo()-returns-may-vary>`{.interpreted-text
    role="ref"}
-   `Possible Infinite Loop <possible-infinite-loop>`{.interpreted-text
    role="ref"}
-   `Possible Missing Subpattern <possible-missing-subpattern>`{.interpreted-text
    role="ref"}
-   `Pre-increment <pre-increment>`{.interpreted-text role="ref"}
-   `Preprocessable <preprocessable>`{.interpreted-text role="ref"}
-   `Print And Die <print-and-die>`{.interpreted-text role="ref"}
-   `Printf Number Of Arguments <printf-number-of-arguments>`{.interpreted-text
    role="ref"}
-   `Property Could Be Local <property-could-be-local>`{.interpreted-text
    role="ref"}
-   `Property Used In One Method Only <property-used-in-one-method-only>`{.interpreted-text
    role="ref"}
-   `Queries In Loops <queries-in-loops>`{.interpreted-text role="ref"}
-   `Randomly Sorted Arrays <randomly-sorted-arrays>`{.interpreted-text
    role="ref"}
-   `Redeclared PHP Functions <redeclared-php-functions>`{.interpreted-text
    role="ref"}
-   `Redefined Class Constants <redefined-class-constants>`{.interpreted-text
    role="ref"}
-   `Redefined Default <redefined-default>`{.interpreted-text
    role="ref"}
-   `Redefined Private Property <redefined-private-property>`{.interpreted-text
    role="ref"}
-   `Relay Function <relay-function>`{.interpreted-text role="ref"}
-   `Repeated Interface <repeated-interface>`{.interpreted-text
    role="ref"}
-   `Repeated Regex <repeated-regex>`{.interpreted-text role="ref"}
-   `Repeated print() <repeated-print()>`{.interpreted-text role="ref"}
-   `Results May Be Missing <results-may-be-missing>`{.interpreted-text
    role="ref"}
-   `Return True False <return-true-false>`{.interpreted-text
    role="ref"}
-   `Same Conditions In Condition <same-conditions-in-condition>`{.interpreted-text
    role="ref"}
-   `Same Variable Foreach <same-variable-foreach>`{.interpreted-text
    role="ref"}
-   `Scalar Are Not Arrays <scalar-are-not-arrays>`{.interpreted-text
    role="ref"}
-   `Scalar Or Object Property <scalar-or-object-property>`{.interpreted-text
    role="ref"}
-   `Several Instructions On The Same Line <several-instructions-on-the-same-line>`{.interpreted-text
    role="ref"}
-   `Short Open Tags <short-open-tags>`{.interpreted-text role="ref"}
-   `Should Chain Exception <should-chain-exception>`{.interpreted-text
    role="ref"}
-   `Should Make Alias <should-make-alias>`{.interpreted-text
    role="ref"}
-   `Should Make Ternary <should-make-ternary>`{.interpreted-text
    role="ref"}
-   `Should Typecast <should-typecast>`{.interpreted-text role="ref"}
-   `Should Use Coalesce <should-use-coalesce>`{.interpreted-text
    role="ref"}
-   `Should Use Constants <should-use-constants>`{.interpreted-text
    role="ref"}
-   `Should Use Explode Args <should-use-explode-args>`{.interpreted-text
    role="ref"}
-   `Should Use Local Class <should-use-local-class>`{.interpreted-text
    role="ref"}
-   `Should Use Prepared Statement <should-use-prepared-statement>`{.interpreted-text
    role="ref"}
-   `Should Use SetCookie() <should-use-setcookie()>`{.interpreted-text
    role="ref"}
-   `Should Yield With Key <should-yield-with-key>`{.interpreted-text
    role="ref"}
-   `Silently Cast Integer <silently-cast-integer>`{.interpreted-text
    role="ref"}
-   `Static Loop <static-loop>`{.interpreted-text role="ref"}
-   `Static Methods Called From Object <static-methods-called-from-object>`{.interpreted-text
    role="ref"}
-   `Static Methods Can't Contain $this <static-methods-can't-contain-$this>`{.interpreted-text
    role="ref"}
-   `Strange Name For Constants <strange-name-for-constants>`{.interpreted-text
    role="ref"}
-   `Strange Name For Variables <strange-name-for-variables>`{.interpreted-text
    role="ref"}
-   `Strict Comparison With Booleans <strict-comparison-with-booleans>`{.interpreted-text
    role="ref"}
-   `String May Hold A Variable <string-may-hold-a-variable>`{.interpreted-text
    role="ref"}
-   `Strings With Strange Space <strings-with-strange-space>`{.interpreted-text
    role="ref"}
-   `Strpos()-like Comparison <strpos()-like-comparison>`{.interpreted-text
    role="ref"}
-   `Strtr Arguments <strtr-arguments>`{.interpreted-text role="ref"}
-   `Suspicious Comparison <suspicious-comparison>`{.interpreted-text
    role="ref"}
-   `Swapped Arguments <swapped-arguments>`{.interpreted-text
    role="ref"}
-   `Switch To Switch <switch-to-switch>`{.interpreted-text role="ref"}
-   `Switch Without Default <switch-without-default>`{.interpreted-text
    role="ref"}
-   `Ternary In Concat <ternary-in-concat>`{.interpreted-text
    role="ref"}
-   `Test Then Cast <test-then-cast>`{.interpreted-text role="ref"}
-   `Throw Functioncall <throw-functioncall>`{.interpreted-text
    role="ref"}
-   `Throw In Destruct <throw-in-destruct>`{.interpreted-text
    role="ref"}
-   `Throws An Assignement <throws-an-assignement>`{.interpreted-text
    role="ref"}
-   `Timestamp Difference <timestamp-difference>`{.interpreted-text
    role="ref"}
-   `Too Many Array Dimensions <too-many-array-dimensions>`{.interpreted-text
    role="ref"}
-   `Too Many Dereferencing <too-many-dereferencing>`{.interpreted-text
    role="ref"}
-   `Too Many Finds <too-many-finds>`{.interpreted-text role="ref"}
-   `Too Many Injections <too-many-injections>`{.interpreted-text
    role="ref"}
-   `Too Many Local Variables <too-many-local-variables>`{.interpreted-text
    role="ref"}
-   `Too Many Native Calls <too-many-native-calls>`{.interpreted-text
    role="ref"}
-   `Trait Not Found <trait-not-found>`{.interpreted-text role="ref"}
-   `Typehint Must Be Returned <typehint-must-be-returned>`{.interpreted-text
    role="ref"}
-   `Typehinted References <typehinted-references>`{.interpreted-text
    role="ref"}
-   `Uncaught Exceptions <uncaught-exceptions>`{.interpreted-text
    role="ref"}
-   `Unchecked Resources <unchecked-resources>`{.interpreted-text
    role="ref"}
-   `Unconditional Break In Loop <unconditional-break-in-loop>`{.interpreted-text
    role="ref"}
-   `Undefined Class Constants <undefined-class-constants>`{.interpreted-text
    role="ref"}
-   `Undefined Classes <undefined-classes>`{.interpreted-text
    role="ref"}
-   `Undefined Constant Name <undefined-constant-name>`{.interpreted-text
    role="ref"}
-   `Undefined Constants <undefined-constants>`{.interpreted-text
    role="ref"}
-   `Undefined Functions <undefined-functions>`{.interpreted-text
    role="ref"}
-   `Undefined Insteadof <undefined-insteadof>`{.interpreted-text
    role="ref"}
-   `Undefined Interfaces <undefined-interfaces>`{.interpreted-text
    role="ref"}
-   `Undefined Parent <undefined-parent>`{.interpreted-text role="ref"}
-   `Undefined Properties <undefined-properties>`{.interpreted-text
    role="ref"}
-   `Undefined Trait <undefined-trait>`{.interpreted-text role="ref"}
-   `Undefined Variable <undefined-variable>`{.interpreted-text
    role="ref"}
-   `Undefined \:\:class <undefined-\:\:class>`{.interpreted-text
    role="ref"}
-   `Undefined static\:\: Or self\:\: <undefined-static\:\:-or-self\:\:>`{.interpreted-text
    role="ref"}
-   `Unknown Parameter Name <unknown-parameter-name>`{.interpreted-text
    role="ref"}
-   `Unknown Pcre2 Option <unknown-pcre2-option>`{.interpreted-text
    role="ref"}
-   `Unkown Regex Options <unkown-regex-options>`{.interpreted-text
    role="ref"}
-   `Unpreprocessed Values <unpreprocessed-values>`{.interpreted-text
    role="ref"}
-   `Unresolved Classes <unresolved-classes>`{.interpreted-text
    role="ref"}
-   `Unresolved Instanceof <unresolved-instanceof>`{.interpreted-text
    role="ref"}
-   `Unresolved Use <unresolved-use>`{.interpreted-text role="ref"}
-   `Unset In Foreach <unset-in-foreach>`{.interpreted-text role="ref"}
-   `Unsupported Types With Operators <unsupported-types-with-operators>`{.interpreted-text
    role="ref"}
-   `Unthrown Exception <unthrown-exception>`{.interpreted-text
    role="ref"}
-   `Unused Arguments <unused-arguments>`{.interpreted-text role="ref"}
-   `Unused Class Constant <unused-class-constant>`{.interpreted-text
    role="ref"}
-   `Unused Classes <unused-classes>`{.interpreted-text role="ref"}
-   `Unused Global <unused-global>`{.interpreted-text role="ref"}
-   `Unused Inherited Variable In Closure <unused-inherited-variable-in-closure>`{.interpreted-text
    role="ref"}
-   `Unused Returned Value <unused-returned-value>`{.interpreted-text
    role="ref"}
-   `Use === null <use-===-null>`{.interpreted-text role="ref"}
-   `Use Constant <use-constant>`{.interpreted-text role="ref"}
-   `Use Constant As Arguments <use-constant-as-arguments>`{.interpreted-text
    role="ref"}
-   `Use Instanceof <use-instanceof>`{.interpreted-text role="ref"}
-   `Use Named Boolean In Argument Definition <use-named-boolean-in-argument-definition>`{.interpreted-text
    role="ref"}
-   `Use PHP Object API <use-php-object-api>`{.interpreted-text
    role="ref"}
-   `Use Pathinfo <use-pathinfo>`{.interpreted-text role="ref"}
-   `Use Positive Condition <use-positive-condition>`{.interpreted-text
    role="ref"}
-   `Use System Tmp <use-system-tmp>`{.interpreted-text role="ref"}
-   `Use With Fully Qualified Name <use-with-fully-qualified-name>`{.interpreted-text
    role="ref"}
-   `Use \:\:Class Operator <use-\:\:class-operator>`{.interpreted-text
    role="ref"}
-   `Use array_slice() <use-array\_slice()>`{.interpreted-text
    role="ref"}
-   `Use const <use-const>`{.interpreted-text role="ref"}
-   `Use random_int() <use-random\_int()>`{.interpreted-text role="ref"}
-   `Used Once Property <used-once-property>`{.interpreted-text
    role="ref"}
-   `Used Once Variables (In Scope) <used-once-variables-(in-scope)>`{.interpreted-text
    role="ref"}
-   `Used Once Variables <used-once-variables>`{.interpreted-text
    role="ref"}
-   `Useless Abstract Class <useless-abstract-class>`{.interpreted-text
    role="ref"}
-   `Useless Alias <useless-alias>`{.interpreted-text role="ref"}
-   `Useless Brackets <useless-brackets>`{.interpreted-text role="ref"}
-   `Useless Catch <useless-catch>`{.interpreted-text role="ref"}
-   `Useless Check <useless-check>`{.interpreted-text role="ref"}
-   `Useless Constructor <useless-constructor>`{.interpreted-text
    role="ref"}
-   `Useless Final <useless-final>`{.interpreted-text role="ref"}
-   `Useless Global <useless-global>`{.interpreted-text role="ref"}
-   `Useless Instructions <useless-instructions>`{.interpreted-text
    role="ref"}
-   `Useless Interfaces <useless-interfaces>`{.interpreted-text
    role="ref"}
-   `Useless Parenthesis <useless-parenthesis>`{.interpreted-text
    role="ref"}
-   `Useless Referenced Argument <useless-referenced-argument>`{.interpreted-text
    role="ref"}
-   `Useless Return <useless-return>`{.interpreted-text role="ref"}
-   `Useless Switch <useless-switch>`{.interpreted-text role="ref"}
-   `Useless Type Casting <useless-type-casting>`{.interpreted-text
    role="ref"}
-   `Useless Unset <useless-unset>`{.interpreted-text role="ref"}
-   `Uses Default Values <uses-default-values>`{.interpreted-text
    role="ref"}
-   `Using $this Outside A Class <using-$this-outside-a-class>`{.interpreted-text
    role="ref"}
-   `Using Deprecated Method <using-deprecated-method>`{.interpreted-text
    role="ref"}
-   `Var Keyword <var-keyword>`{.interpreted-text role="ref"}
-   `Variable Is Not A Condition <variable-is-not-a-condition>`{.interpreted-text
    role="ref"}
-   `Weak Typing <weak-typing>`{.interpreted-text role="ref"}
-   `While(List() = Each()) <while(list()-=-each())>`{.interpreted-text
    role="ref"}
-   `Written Only Variables <written-only-variables>`{.interpreted-text
    role="ref"}
-   `Wrong Access Style to Property <wrong-access-style-to-property>`{.interpreted-text
    role="ref"}
-   `Wrong Argument Type <wrong-argument-type>`{.interpreted-text
    role="ref"}
-   `Wrong Attribute Configuration <wrong-attribute-configuration>`{.interpreted-text
    role="ref"}
-   `Wrong Number Of Arguments <wrong-number-of-arguments>`{.interpreted-text
    role="ref"}
-   `Wrong Optional Parameter <wrong-optional-parameter>`{.interpreted-text
    role="ref"}
-   `Wrong Parameter Type <wrong-parameter-type>`{.interpreted-text
    role="ref"}
-   `Wrong Range Check <wrong-range-check>`{.interpreted-text
    role="ref"}
-   `Wrong Type For Native PHP Function <wrong-type-for-native-php-function>`{.interpreted-text
    role="ref"}
-   `Wrong Type Returned <wrong-type-returned>`{.interpreted-text
    role="ref"}
-   `Wrong Type With Call <wrong-type-with-call>`{.interpreted-text
    role="ref"}
-   `Wrong Typed Property Default <wrong-typed-property-default>`{.interpreted-text
    role="ref"}
-   `Wrong fopen() Mode <wrong-fopen()-mode>`{.interpreted-text
    role="ref"}
-   `__DIR__ Then Slash <\_\_dir\_\_-then-slash>`{.interpreted-text
    role="ref"}
-   `__toString() Throws Exception <\_\_tostring()-throws-exception>`{.interpreted-text
    role="ref"}
-   `array_key_exists() Works On Arrays <array\_key\_exists()-works-on-arrays>`{.interpreted-text
    role="ref"}
-   `array_merge() And Variadic <array\_merge()-and-variadic>`{.interpreted-text
    role="ref"}
-   `error_reporting() With Integers <error\_reporting()-with-integers>`{.interpreted-text
    role="ref"}
-   `eval() Without Try <eval()-without-try>`{.interpreted-text
    role="ref"}
-   `func_get_arg() Modified <func\_get\_arg()-modified>`{.interpreted-text
    role="ref"}
-   `include_once() Usage <include\_once()-usage>`{.interpreted-text
    role="ref"}
-   `list() May Omit Variables <list()-may-omit-variables>`{.interpreted-text
    role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}
-   `self, parent, static Outside Class <self,-parent,-static-outside-class>`{.interpreted-text
    role="ref"}
-   `strip_tags Skips Closed Tag <strip\_tags-skips-closed-tag>`{.interpreted-text
    role="ref"}
-   `strpos() Too Much <strpos()-too-much>`{.interpreted-text
    role="ref"}
-   `var_dump()... Usage <var\_dump()...-usage>`{.interpreted-text
    role="ref"}

### CI-checks

This ruleset is a collection of important rules to run in a CI pipeline.

Total : 177 analysis

-   `@ Operator <@-operator>`{.interpreted-text role="ref"}
-   `Adding Zero <adding-zero>`{.interpreted-text role="ref"}
-   `Aliases Usage <aliases-usage>`{.interpreted-text role="ref"}
-   `Altering Foreach Without Reference <altering-foreach-without-reference>`{.interpreted-text
    role="ref"}
-   `Always Positive Comparison <always-positive-comparison>`{.interpreted-text
    role="ref"}
-   `Assign And Compare <assign-and-compare>`{.interpreted-text
    role="ref"}
-   `Assign With And Precedence <assign-with-and-precedence>`{.interpreted-text
    role="ref"}
-   `Avoid Parenthesis <avoid-parenthesis>`{.interpreted-text
    role="ref"}
-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Avoid get_class() <avoid-get\_class()>`{.interpreted-text
    role="ref"}
-   `Callback Function Needs Return <callback-function-needs-return>`{.interpreted-text
    role="ref"}
-   `Cant Implement Traversable <cant-implement-traversable>`{.interpreted-text
    role="ref"}
-   `Casting Ternary <casting-ternary>`{.interpreted-text role="ref"}
-   `Check JSON <check-json>`{.interpreted-text role="ref"}
-   `Check On __Call Usage <check-on-\_\_call-usage>`{.interpreted-text
    role="ref"}
-   `Class Without Parent <class-without-parent>`{.interpreted-text
    role="ref"}
-   `Coalesce And Concat <coalesce-and-concat>`{.interpreted-text
    role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Constant Class <constant-class>`{.interpreted-text role="ref"}
-   `Constants With Strange Names <constants-with-strange-names>`{.interpreted-text
    role="ref"}
-   `Could Use Short Assignation <could-use-short-assignation>`{.interpreted-text
    role="ref"}
-   `Could Use __DIR__ <could-use-\_\_dir\_\_>`{.interpreted-text
    role="ref"}
-   `Could Use str_repeat() <could-use-str\_repeat()>`{.interpreted-text
    role="ref"}
-   `Dangling Array References <dangling-array-references>`{.interpreted-text
    role="ref"}
-   `Deprecated PHP Functions <deprecated-php-functions>`{.interpreted-text
    role="ref"}
-   `Don't Echo Error <don't-echo-error>`{.interpreted-text role="ref"}
-   `Don't Unset Properties <don't-unset-properties>`{.interpreted-text
    role="ref"}
-   `Drop Else After Return <drop-else-after-return>`{.interpreted-text
    role="ref"}
-   `Else If Versus Elseif <else-if-versus-elseif>`{.interpreted-text
    role="ref"}
-   `Empty Blocks <empty-blocks>`{.interpreted-text role="ref"}
-   `Empty Namespace <empty-namespace>`{.interpreted-text role="ref"}
-   `Exit() Usage <exit()-usage>`{.interpreted-text role="ref"}
-   `Failed Substr Comparison <failed-substr-comparison>`{.interpreted-text
    role="ref"}
-   `Foreach Reference Is Not Modified <foreach-reference-is-not-modified>`{.interpreted-text
    role="ref"}
-   `Forgotten Visibility <forgotten-visibility>`{.interpreted-text
    role="ref"}
-   `Forgotten Whitespace <forgotten-whitespace>`{.interpreted-text
    role="ref"}
-   `Hidden Use Expression <hidden-use-expression>`{.interpreted-text
    role="ref"}
-   `Htmlentities Calls <htmlentities-calls>`{.interpreted-text
    role="ref"}
-   `Identical Conditions <identical-conditions>`{.interpreted-text
    role="ref"}
-   `Identical On Both Sides <identical-on-both-sides>`{.interpreted-text
    role="ref"}
-   `If With Same Conditions <if-with-same-conditions>`{.interpreted-text
    role="ref"}
-   `Implied If <implied-if>`{.interpreted-text role="ref"}
-   `Implode() Arguments Order <implode()-arguments-order>`{.interpreted-text
    role="ref"}
-   `Indices Are Int Or String <indices-are-int-or-string>`{.interpreted-text
    role="ref"}
-   `Interfaces Is Not Implemented <interfaces-is-not-implemented>`{.interpreted-text
    role="ref"}
-   `Invalid Pack Format <invalid-pack-format>`{.interpreted-text
    role="ref"}
-   `Invalid Regex <invalid-regex>`{.interpreted-text role="ref"}
-   `Is Actually Zero <is-actually-zero>`{.interpreted-text role="ref"}
-   `Is_A() With String <is\_a()-with-string>`{.interpreted-text
    role="ref"}
-   `Logical Mistakes <logical-mistakes>`{.interpreted-text role="ref"}
-   `Logical Should Use Symbolic Operators <logical-should-use-symbolic-operators>`{.interpreted-text
    role="ref"}
-   `Lone Blocks <lone-blocks>`{.interpreted-text role="ref"}
-   `Mbstring Third Arg <mbstring-third-arg>`{.interpreted-text
    role="ref"}
-   `Mbstring Unknown Encoding <mbstring-unknown-encoding>`{.interpreted-text
    role="ref"}
-   `Merge If Then <merge-if-then>`{.interpreted-text role="ref"}
-   `Missing Parenthesis <missing-parenthesis>`{.interpreted-text
    role="ref"}
-   `Missing Some Returntype <missing-some-returntype>`{.interpreted-text
    role="ref"}
-   `Multiple Alias Definitions <multiple-alias-definitions>`{.interpreted-text
    role="ref"}
-   `Multiple Alias Definitions Per File <multiple-alias-definitions-per-file>`{.interpreted-text
    role="ref"}
-   `Multiple Class Declarations <multiple-class-declarations>`{.interpreted-text
    role="ref"}
-   `Multiple Constant Definition <multiple-constant-definition>`{.interpreted-text
    role="ref"}
-   `Multiple Identical Trait Or Interface <multiple-identical-trait-or-interface>`{.interpreted-text
    role="ref"}
-   `Multiple Index Definition <multiple-index-definition>`{.interpreted-text
    role="ref"}
-   `Multiples Identical Case <multiples-identical-case>`{.interpreted-text
    role="ref"}
-   `Multiply By One <multiply-by-one>`{.interpreted-text role="ref"}
-   `Must Return Methods <must-return-methods>`{.interpreted-text
    role="ref"}
-   `Negative Power <negative-power>`{.interpreted-text role="ref"}
-   `Nested Ternary <nested-ternary>`{.interpreted-text role="ref"}
-   `Next Month Trap <next-month-trap>`{.interpreted-text role="ref"}
-   `No Choice <no-choice>`{.interpreted-text role="ref"}
-   `No Class In Global <no-class-in-global>`{.interpreted-text
    role="ref"}
-   `No Direct Call To Magic Method <no-direct-call-to-magic-method>`{.interpreted-text
    role="ref"}
-   `No Empty Regex <no-empty-regex>`{.interpreted-text role="ref"}
-   `No Literal For Reference <no-literal-for-reference>`{.interpreted-text
    role="ref"}
-   `No Magic Method With Array <no-magic-method-with-array>`{.interpreted-text
    role="ref"}
-   `No Parenthesis For Language Construct <no-parenthesis-for-language-construct>`{.interpreted-text
    role="ref"}
-   `No Real Comparison <no-real-comparison>`{.interpreted-text
    role="ref"}
-   `No Reference For Ternary <no-reference-for-ternary>`{.interpreted-text
    role="ref"}
-   `No Reference On Left Side <no-reference-on-left-side>`{.interpreted-text
    role="ref"}
-   `No array_merge() In Loops <no-array\_merge()-in-loops>`{.interpreted-text
    role="ref"}
-   `No isset() With empty() <no-isset()-with-empty()>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Not Equal Is Not !== <not-equal-is-not-!==>`{.interpreted-text
    role="ref"}
-   `Not Not <not-not>`{.interpreted-text role="ref"}
-   `Objects Don't Need References <objects-don't-need-references>`{.interpreted-text
    role="ref"}
-   `One Variable String <one-variable-string>`{.interpreted-text
    role="ref"}
-   `Or Die <or-die>`{.interpreted-text role="ref"}
-   `Overwritten Exceptions <overwritten-exceptions>`{.interpreted-text
    role="ref"}
-   `Possible Missing Subpattern <possible-missing-subpattern>`{.interpreted-text
    role="ref"}
-   `Pre-increment <pre-increment>`{.interpreted-text role="ref"}
-   `Print And Die <print-and-die>`{.interpreted-text role="ref"}
-   `Printf Number Of Arguments <printf-number-of-arguments>`{.interpreted-text
    role="ref"}
-   `Redeclared PHP Functions <redeclared-php-functions>`{.interpreted-text
    role="ref"}
-   `Redefined Class Constants <redefined-class-constants>`{.interpreted-text
    role="ref"}
-   `Redefined Default <redefined-default>`{.interpreted-text
    role="ref"}
-   `Repeated Regex <repeated-regex>`{.interpreted-text role="ref"}
-   `Repeated print() <repeated-print()>`{.interpreted-text role="ref"}
-   `Results May Be Missing <results-may-be-missing>`{.interpreted-text
    role="ref"}
-   `Return True False <return-true-false>`{.interpreted-text
    role="ref"}
-   `Same Conditions In Condition <same-conditions-in-condition>`{.interpreted-text
    role="ref"}
-   `Same Variable Foreach <same-variable-foreach>`{.interpreted-text
    role="ref"}
-   `Scalar Are Not Arrays <scalar-are-not-arrays>`{.interpreted-text
    role="ref"}
-   `Should Chain Exception <should-chain-exception>`{.interpreted-text
    role="ref"}
-   `Should Make Alias <should-make-alias>`{.interpreted-text
    role="ref"}
-   `Should Make Ternary <should-make-ternary>`{.interpreted-text
    role="ref"}
-   `Should Typecast <should-typecast>`{.interpreted-text role="ref"}
-   `Should Use Coalesce <should-use-coalesce>`{.interpreted-text
    role="ref"}
-   `Should Use Explode Args <should-use-explode-args>`{.interpreted-text
    role="ref"}
-   `Should Use Prepared Statement <should-use-prepared-statement>`{.interpreted-text
    role="ref"}
-   `Should Yield With Key <should-yield-with-key>`{.interpreted-text
    role="ref"}
-   `Silently Cast Integer <silently-cast-integer>`{.interpreted-text
    role="ref"}
-   `Static Methods Called From Object <static-methods-called-from-object>`{.interpreted-text
    role="ref"}
-   `Static Methods Can't Contain $this <static-methods-can't-contain-$this>`{.interpreted-text
    role="ref"}
-   `Strict Comparison With Booleans <strict-comparison-with-booleans>`{.interpreted-text
    role="ref"}
-   `Strings With Strange Space <strings-with-strange-space>`{.interpreted-text
    role="ref"}
-   `Strpos()-like Comparison <strpos()-like-comparison>`{.interpreted-text
    role="ref"}
-   `Strtr Arguments <strtr-arguments>`{.interpreted-text role="ref"}
-   `Switch Without Default <switch-without-default>`{.interpreted-text
    role="ref"}
-   `Ternary In Concat <ternary-in-concat>`{.interpreted-text
    role="ref"}
-   `Throw Functioncall <throw-functioncall>`{.interpreted-text
    role="ref"}
-   `Throw In Destruct <throw-in-destruct>`{.interpreted-text
    role="ref"}
-   `Throws An Assignement <throws-an-assignement>`{.interpreted-text
    role="ref"}
-   `Timestamp Difference <timestamp-difference>`{.interpreted-text
    role="ref"}
-   `Typehint Must Be Returned <typehint-must-be-returned>`{.interpreted-text
    role="ref"}
-   `Typehinted References <typehinted-references>`{.interpreted-text
    role="ref"}
-   `Unchecked Resources <unchecked-resources>`{.interpreted-text
    role="ref"}
-   `Unconditional Break In Loop <unconditional-break-in-loop>`{.interpreted-text
    role="ref"}
-   `Undefined Class Constants <undefined-class-constants>`{.interpreted-text
    role="ref"}
-   `Undefined Constants <undefined-constants>`{.interpreted-text
    role="ref"}
-   `Undefined Functions <undefined-functions>`{.interpreted-text
    role="ref"}
-   `Undefined Insteadof <undefined-insteadof>`{.interpreted-text
    role="ref"}
-   `Undefined Interfaces <undefined-interfaces>`{.interpreted-text
    role="ref"}
-   `Undefined Properties <undefined-properties>`{.interpreted-text
    role="ref"}
-   `Undefined Trait <undefined-trait>`{.interpreted-text role="ref"}
-   `Undefined Variable <undefined-variable>`{.interpreted-text
    role="ref"}
-   `Undefined \:\:class <undefined-\:\:class>`{.interpreted-text
    role="ref"}
-   `Unknown Parameter Name <unknown-parameter-name>`{.interpreted-text
    role="ref"}
-   `Unused Inherited Variable In Closure <unused-inherited-variable-in-closure>`{.interpreted-text
    role="ref"}
-   `Use === null <use-===-null>`{.interpreted-text role="ref"}
-   `Use Constant <use-constant>`{.interpreted-text role="ref"}
-   `Use Constant As Arguments <use-constant-as-arguments>`{.interpreted-text
    role="ref"}
-   `Use Instanceof <use-instanceof>`{.interpreted-text role="ref"}
-   `Use PHP Object API <use-php-object-api>`{.interpreted-text
    role="ref"}
-   `Use Pathinfo <use-pathinfo>`{.interpreted-text role="ref"}
-   `Use System Tmp <use-system-tmp>`{.interpreted-text role="ref"}
-   `Use \:\:Class Operator <use-\:\:class-operator>`{.interpreted-text
    role="ref"}
-   `Use array_slice() <use-array\_slice()>`{.interpreted-text
    role="ref"}
-   `Use const <use-const>`{.interpreted-text role="ref"}
-   `Use random_int() <use-random\_int()>`{.interpreted-text role="ref"}
-   `Useless Alias <useless-alias>`{.interpreted-text role="ref"}
-   `Useless Brackets <useless-brackets>`{.interpreted-text role="ref"}
-   `Useless Catch <useless-catch>`{.interpreted-text role="ref"}
-   `Useless Check <useless-check>`{.interpreted-text role="ref"}
-   `Useless Final <useless-final>`{.interpreted-text role="ref"}
-   `Useless Instructions <useless-instructions>`{.interpreted-text
    role="ref"}
-   `Useless Parenthesis <useless-parenthesis>`{.interpreted-text
    role="ref"}
-   `Useless Type Casting <useless-type-casting>`{.interpreted-text
    role="ref"}
-   `Useless Unset <useless-unset>`{.interpreted-text role="ref"}
-   `Uses Default Values <uses-default-values>`{.interpreted-text
    role="ref"}
-   `While(List() = Each()) <while(list()-=-each())>`{.interpreted-text
    role="ref"}
-   `Wrong Access Style to Property <wrong-access-style-to-property>`{.interpreted-text
    role="ref"}
-   `Wrong Number Of Arguments <wrong-number-of-arguments>`{.interpreted-text
    role="ref"}
-   `Wrong Optional Parameter <wrong-optional-parameter>`{.interpreted-text
    role="ref"}
-   `Wrong Parameter Type <wrong-parameter-type>`{.interpreted-text
    role="ref"}
-   `Wrong Type For Native PHP Function <wrong-type-for-native-php-function>`{.interpreted-text
    role="ref"}
-   `Wrong Type Returned <wrong-type-returned>`{.interpreted-text
    role="ref"}
-   `Wrong Type With Call <wrong-type-with-call>`{.interpreted-text
    role="ref"}
-   `Wrong Typed Property Default <wrong-typed-property-default>`{.interpreted-text
    role="ref"}
-   `Wrong fopen() Mode <wrong-fopen()-mode>`{.interpreted-text
    role="ref"}
-   `__DIR__ Then Slash <\_\_dir\_\_-then-slash>`{.interpreted-text
    role="ref"}
-   `error_reporting() With Integers <error\_reporting()-with-integers>`{.interpreted-text
    role="ref"}
-   `eval() Without Try <eval()-without-try>`{.interpreted-text
    role="ref"}
-   `list() May Omit Variables <list()-may-omit-variables>`{.interpreted-text
    role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}
-   `strip_tags Skips Closed Tag <strip\_tags-skips-closed-tag>`{.interpreted-text
    role="ref"}
-   `strpos() Too Much <strpos()-too-much>`{.interpreted-text
    role="ref"}
-   `var_dump()... Usage <var\_dump()...-usage>`{.interpreted-text
    role="ref"}

### ClassReview

This ruleset focuses on classes construction issues, and their related
structures : traits, interfaces, methods, properties, constants.

Total : 51 analysis

-   `Avoid Self In Interface <avoid-self-in-interface>`{.interpreted-text
    role="ref"}
-   `Avoid option arrays in constructors <avoid-option-arrays-in-constructors>`{.interpreted-text
    role="ref"}
-   `Cancel Common Method <cancel-common-method>`{.interpreted-text
    role="ref"}
-   `Class Could Be Final <class-could-be-final>`{.interpreted-text
    role="ref"}
-   `Class Without Parent <class-without-parent>`{.interpreted-text
    role="ref"}
-   `Classes Mutually Extending Each Other <classes-mutually-extending-each-other>`{.interpreted-text
    role="ref"}
-   `Could Be Abstract Class <could-be-abstract-class>`{.interpreted-text
    role="ref"}
-   `Could Be Class Constant <could-be-class-constant>`{.interpreted-text
    role="ref"}
-   `Could Be Parent Method <could-be-parent-method>`{.interpreted-text
    role="ref"}
-   `Could Be Private Class Constant <could-be-private-class-constant>`{.interpreted-text
    role="ref"}
-   `Could Be Protected Class Constant <could-be-protected-class-constant>`{.interpreted-text
    role="ref"}
-   `Could Be Protected Method <could-be-protected-method>`{.interpreted-text
    role="ref"}
-   `Could Be Protected Property <could-be-protected-property>`{.interpreted-text
    role="ref"}
-   `Could Be Static <could-be-static>`{.interpreted-text role="ref"}
-   `Could Use self <could-use-self>`{.interpreted-text role="ref"}
-   `Cyclic References <cyclic-references>`{.interpreted-text
    role="ref"}
-   `Dependant Abstract Classes <dependant-abstract-classes>`{.interpreted-text
    role="ref"}
-   `Different Argument Counts <different-argument-counts>`{.interpreted-text
    role="ref"}
-   `Disconnected Classes <disconnected-classes>`{.interpreted-text
    role="ref"}
-   `Double Object Assignation <double-object-assignation>`{.interpreted-text
    role="ref"}
-   `Exceeding Typehint <exceeding-typehint>`{.interpreted-text
    role="ref"}
-   `Final Class Usage <final-class-usage>`{.interpreted-text
    role="ref"}
-   `Final Methods Usage <final-methods-usage>`{.interpreted-text
    role="ref"}
-   `Fossilized Method <fossilized-method>`{.interpreted-text
    role="ref"}
-   `Hidden Nullable <hidden-nullable>`{.interpreted-text role="ref"}
-   `Insufficient Property Typehint <insufficient-property-typehint>`{.interpreted-text
    role="ref"}
-   `Interfaces Don't Ensure Properties <interfaces-don't-ensure-properties>`{.interpreted-text
    role="ref"}
-   `Interfaces Is Not Implemented <interfaces-is-not-implemented>`{.interpreted-text
    role="ref"}
-   `Memoize MagicCall <memoize-magiccall>`{.interpreted-text
    role="ref"}
-   `Method Could Be Private Method <method-could-be-private-method>`{.interpreted-text
    role="ref"}
-   `Method Could Be Static <method-could-be-static>`{.interpreted-text
    role="ref"}
-   `Mismatch Properties Typehints <mismatch-properties-typehints>`{.interpreted-text
    role="ref"}
-   `Missing Abstract Method <missing-abstract-method>`{.interpreted-text
    role="ref"}
-   `Modified Typed Parameter <modified-typed-parameter>`{.interpreted-text
    role="ref"}
-   `No Self Referencing Constant <no-self-referencing-constant>`{.interpreted-text
    role="ref"}
-   `Non Nullable Getters <non-nullable-getters>`{.interpreted-text
    role="ref"}
-   `Nullable Without Check <nullable-without-check>`{.interpreted-text
    role="ref"}
-   `Property Could Be Local <property-could-be-local>`{.interpreted-text
    role="ref"}
-   `Property Could Be Private Property <property-could-be-private-property>`{.interpreted-text
    role="ref"}
-   `Raised Access Level <raised-access-level>`{.interpreted-text
    role="ref"}
-   `Redefined Property <redefined-property>`{.interpreted-text
    role="ref"}
-   `Self Using Trait <self-using-trait>`{.interpreted-text role="ref"}
-   `Uninitilized Property <uninitilized-property>`{.interpreted-text
    role="ref"}
-   `Unreachable Class Constant <unreachable-class-constant>`{.interpreted-text
    role="ref"}
-   `Unused Class Constant <unused-class-constant>`{.interpreted-text
    role="ref"}
-   `Unused Trait In Class <unused-trait-in-class>`{.interpreted-text
    role="ref"}
-   `Useless Interfaces <useless-interfaces>`{.interpreted-text
    role="ref"}
-   `Useless Typehint <useless-typehint>`{.interpreted-text role="ref"}
-   `Wrong Access Style to Property <wrong-access-style-to-property>`{.interpreted-text
    role="ref"}
-   `Wrong Type Returned <wrong-type-returned>`{.interpreted-text
    role="ref"}
-   `Wrong Typed Property Default <wrong-typed-property-default>`{.interpreted-text
    role="ref"}

### Coding Conventions

This ruleset centralizes all analysis related to coding conventions.
Sometimes, those are easy to extract with static analysis, and so here
they are. No all o them are available.

Total : 27 analysis

-   `All Uppercase Variables <all-uppercase-variables>`{.interpreted-text
    role="ref"}
-   `Bracketless Blocks <bracketless-blocks>`{.interpreted-text
    role="ref"}
-   `Close Tags <close-tags>`{.interpreted-text role="ref"}
-   `Constant Comparison <constant-comparison>`{.interpreted-text
    role="ref"}
-   `Don't Be Too Manual <don't-be-too-manual>`{.interpreted-text
    role="ref"}
-   `Echo Or Print <echo-or-print>`{.interpreted-text role="ref"}
-   `Empty Slots In Arrays <empty-slots-in-arrays>`{.interpreted-text
    role="ref"}
-   `Heredoc Delimiter <heredoc-delimiter>`{.interpreted-text
    role="ref"}
-   `Interpolation <interpolation>`{.interpreted-text role="ref"}
-   `Mistaken Concatenation <mistaken-concatenation>`{.interpreted-text
    role="ref"}
-   `Mixed Concat And Interpolation <mixed-concat-and-interpolation>`{.interpreted-text
    role="ref"}
-   `Multiple Classes In One File <multiple-classes-in-one-file>`{.interpreted-text
    role="ref"}
-   `No Plus One <no-plus-one>`{.interpreted-text role="ref"}
-   `Non-lowercase Keywords <non-lowercase-keywords>`{.interpreted-text
    role="ref"}
-   `One Letter Functions <one-letter-functions>`{.interpreted-text
    role="ref"}
-   `Order Of Declaration <order-of-declaration>`{.interpreted-text
    role="ref"}
-   `Return With Parenthesis <return-with-parenthesis>`{.interpreted-text
    role="ref"}
-   `Should Be Single Quote <should-be-single-quote>`{.interpreted-text
    role="ref"}
-   `Similar Integers <similar-integers>`{.interpreted-text role="ref"}
-   `Unusual Case For PHP Functions <unusual-case-for-php-functions>`{.interpreted-text
    role="ref"}
-   `Use With Fully Qualified Name <use-with-fully-qualified-name>`{.interpreted-text
    role="ref"}
-   `Use const <use-const>`{.interpreted-text role="ref"}
-   `Wrong Case Namespaces <wrong-case-namespaces>`{.interpreted-text
    role="ref"}
-   `Wrong Class Name Case <wrong-class-name-case>`{.interpreted-text
    role="ref"}
-   `Wrong Function Name Case <wrong-function-name-case>`{.interpreted-text
    role="ref"}
-   `Wrong Typehinted Name <wrong-typehinted-name>`{.interpreted-text
    role="ref"}
-   `Yoda Comparison <yoda-comparison>`{.interpreted-text role="ref"}

### CompatibilityPHP53

This ruleset centralizes all analysis for the migration from PHP 5.2 to
5.3.

Total : 79 analysis

-   `Anonymous Classes <anonymous-classes>`{.interpreted-text
    role="ref"}
-   `Binary Glossary <binary-glossary>`{.interpreted-text role="ref"}
-   `Break With 0 <break-with-0>`{.interpreted-text role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Cant Use Return Value In Write Context <cant-use-return-value-in-write-context>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Class Const With Array <class-const-with-array>`{.interpreted-text
    role="ref"}
-   `Closure May Use $this <closure-may-use-$this>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Const Visibility Usage <const-visibility-usage>`{.interpreted-text
    role="ref"}
-   `Const With Array <const-with-array>`{.interpreted-text role="ref"}
-   `Constant Scalar Expressions <constant-scalar-expressions>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Define With Array <define-with-array>`{.interpreted-text
    role="ref"}
-   `Dereferencing String And Arrays <dereferencing-string-and-arrays>`{.interpreted-text
    role="ref"}
-   `Direct Call To __clone() <direct-call-to-\_\_clone()>`{.interpreted-text
    role="ref"}
-   `Ellipsis Usage <ellipsis-usage>`{.interpreted-text role="ref"}
-   `Exponent Usage <exponent-usage>`{.interpreted-text role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Foreach With list() <foreach-with-list()>`{.interpreted-text
    role="ref"}
-   `Function Subscripting <function-subscripting>`{.interpreted-text
    role="ref"}
-   `Generator Cannot Return <generator-cannot-return>`{.interpreted-text
    role="ref"}
-   `Group Use Declaration <group-use-declaration>`{.interpreted-text
    role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.1- <hash-algorithms-incompatible-with-php-7.1->`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `List Short Syntax <list-short-syntax>`{.interpreted-text
    role="ref"}
-   `List With Keys <list-with-keys>`{.interpreted-text role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `Malformed Octal <malformed-octal>`{.interpreted-text role="ref"}
-   `Methodcall On New <methodcall-on-new>`{.interpreted-text
    role="ref"}
-   `Mixed Keys Arrays <mixed-keys-arrays>`{.interpreted-text
    role="ref"}
-   `Multiple Definition Of The Same Argument <multiple-definition-of-the-same-argument>`{.interpreted-text
    role="ref"}
-   `Multiple Exceptions Catch() <multiple-exceptions-catch()>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.4 <new-functions-in-php-5.4>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.5 <new-functions-in-php-5.5>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.6 <new-functions-in-php-5.6>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.0 <new-functions-in-php-7.0>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No List With String <no-list-with-string>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No Return For Generator <no-return-for-generator>`{.interpreted-text
    role="ref"}
-   `No String With Append <no-string-with-append>`{.interpreted-text
    role="ref"}
-   `No Substr Minus One <no-substr-minus-one>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Null On New <null-on-new>`{.interpreted-text role="ref"}
-   `PHP 7.0 New Classes <php-7.0-new-classes>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 New Interfaces <php-7.0-new-interfaces>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Scalar Typehints <php-7.0-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Scalar Typehints <php-7.1-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `PHP5 Indirect Variable Expression <php5-indirect-variable-expression>`{.interpreted-text
    role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Parenthesis As Parameter <parenthesis-as-parameter>`{.interpreted-text
    role="ref"}
-   `Php 7 Indirect Expression <php-7-indirect-expression>`{.interpreted-text
    role="ref"}
-   `Php 7.1 New Class <php-7.1-new-class>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php7 Relaxed Keyword <php7-relaxed-keyword>`{.interpreted-text
    role="ref"}
-   `Short Syntax For Arrays <short-syntax-for-arrays>`{.interpreted-text
    role="ref"}
-   `Switch With Too Many Default <switch-with-too-many-default>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Partial <unicode-escape-partial>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Syntax <unicode-escape-syntax>`{.interpreted-text
    role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use Const And Functions <use-const-and-functions>`{.interpreted-text
    role="ref"}
-   `Use Lower Case For Parent, Static And Self <use-lower-case-for-parent,-static-and-self>`{.interpreted-text
    role="ref"}
-   `Use Nullable Type <use-nullable-type>`{.interpreted-text
    role="ref"}
-   `Variable Global <variable-global>`{.interpreted-text role="ref"}
-   `\:\:class <\:\:class>`{.interpreted-text role="ref"}
-   `__debugInfo() Usage <\_\_debuginfo()-usage>`{.interpreted-text
    role="ref"}
-   `ext/dba <ext/dba>`{.interpreted-text role="ref"}
-   `ext/fdf <ext/fdf>`{.interpreted-text role="ref"}
-   `ext/ming <ext/ming>`{.interpreted-text role="ref"}
-   `isset() With Constant <isset()-with-constant>`{.interpreted-text
    role="ref"}

### CompatibilityPHP54

This ruleset centralizes all analysis for the migration from PHP 5.3 to
5.4.

Total : 75 analysis

-   `Anonymous Classes <anonymous-classes>`{.interpreted-text
    role="ref"}
-   `Break With Non Integer <break-with-non-integer>`{.interpreted-text
    role="ref"}
-   `Calltime Pass By Reference <calltime-pass-by-reference>`{.interpreted-text
    role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Cant Use Return Value In Write Context <cant-use-return-value-in-write-context>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Class Const With Array <class-const-with-array>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Const Visibility Usage <const-visibility-usage>`{.interpreted-text
    role="ref"}
-   `Const With Array <const-with-array>`{.interpreted-text role="ref"}
-   `Constant Scalar Expressions <constant-scalar-expressions>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Define With Array <define-with-array>`{.interpreted-text
    role="ref"}
-   `Dereferencing String And Arrays <dereferencing-string-and-arrays>`{.interpreted-text
    role="ref"}
-   `Direct Call To __clone() <direct-call-to-\_\_clone()>`{.interpreted-text
    role="ref"}
-   `Ellipsis Usage <ellipsis-usage>`{.interpreted-text role="ref"}
-   `Exponent Usage <exponent-usage>`{.interpreted-text role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Foreach With list() <foreach-with-list()>`{.interpreted-text
    role="ref"}
-   `Functions Removed In PHP 5.4 <functions-removed-in-php-5.4>`{.interpreted-text
    role="ref"}
-   `Generator Cannot Return <generator-cannot-return>`{.interpreted-text
    role="ref"}
-   `Group Use Declaration <group-use-declaration>`{.interpreted-text
    role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.1- <hash-algorithms-incompatible-with-php-7.1->`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `List Short Syntax <list-short-syntax>`{.interpreted-text
    role="ref"}
-   `List With Keys <list-with-keys>`{.interpreted-text role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `Malformed Octal <malformed-octal>`{.interpreted-text role="ref"}
-   `Mixed Keys Arrays <mixed-keys-arrays>`{.interpreted-text
    role="ref"}
-   `Multiple Definition Of The Same Argument <multiple-definition-of-the-same-argument>`{.interpreted-text
    role="ref"}
-   `Multiple Exceptions Catch() <multiple-exceptions-catch()>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.5 <new-functions-in-php-5.5>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.6 <new-functions-in-php-5.6>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.0 <new-functions-in-php-7.0>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No List With String <no-list-with-string>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No Return For Generator <no-return-for-generator>`{.interpreted-text
    role="ref"}
-   `No String With Append <no-string-with-append>`{.interpreted-text
    role="ref"}
-   `No Substr Minus One <no-substr-minus-one>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Null On New <null-on-new>`{.interpreted-text role="ref"}
-   `PHP 7.0 New Classes <php-7.0-new-classes>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 New Interfaces <php-7.0-new-interfaces>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Scalar Typehints <php-7.0-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Scalar Typehints <php-7.1-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `PHP5 Indirect Variable Expression <php5-indirect-variable-expression>`{.interpreted-text
    role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Parenthesis As Parameter <parenthesis-as-parameter>`{.interpreted-text
    role="ref"}
-   `Php 7 Indirect Expression <php-7-indirect-expression>`{.interpreted-text
    role="ref"}
-   `Php 7.1 New Class <php-7.1-new-class>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php7 Relaxed Keyword <php7-relaxed-keyword>`{.interpreted-text
    role="ref"}
-   `Switch With Too Many Default <switch-with-too-many-default>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Partial <unicode-escape-partial>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Syntax <unicode-escape-syntax>`{.interpreted-text
    role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use Const And Functions <use-const-and-functions>`{.interpreted-text
    role="ref"}
-   `Use Lower Case For Parent, Static And Self <use-lower-case-for-parent,-static-and-self>`{.interpreted-text
    role="ref"}
-   `Use Nullable Type <use-nullable-type>`{.interpreted-text
    role="ref"}
-   `Variable Global <variable-global>`{.interpreted-text role="ref"}
-   `\:\:class <\:\:class>`{.interpreted-text role="ref"}
-   `__debugInfo() Usage <\_\_debuginfo()-usage>`{.interpreted-text
    role="ref"}
-   `crypt() Without Salt <crypt()-without-salt>`{.interpreted-text
    role="ref"}
-   `ext/mhash <ext/mhash>`{.interpreted-text role="ref"}
-   `isset() With Constant <isset()-with-constant>`{.interpreted-text
    role="ref"}

### CompatibilityPHP55

This ruleset centralizes all analysis for the migration from PHP 5.4 to
5.5.

Total : 67 analysis

-   `Anonymous Classes <anonymous-classes>`{.interpreted-text
    role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Class Const With Array <class-const-with-array>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Const Visibility Usage <const-visibility-usage>`{.interpreted-text
    role="ref"}
-   `Const With Array <const-with-array>`{.interpreted-text role="ref"}
-   `Constant Scalar Expressions <constant-scalar-expressions>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Define With Array <define-with-array>`{.interpreted-text
    role="ref"}
-   `Direct Call To __clone() <direct-call-to-\_\_clone()>`{.interpreted-text
    role="ref"}
-   `Ellipsis Usage <ellipsis-usage>`{.interpreted-text role="ref"}
-   `Exponent Usage <exponent-usage>`{.interpreted-text role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Functions Removed In PHP 5.5 <functions-removed-in-php-5.5>`{.interpreted-text
    role="ref"}
-   `Generator Cannot Return <generator-cannot-return>`{.interpreted-text
    role="ref"}
-   `Group Use Declaration <group-use-declaration>`{.interpreted-text
    role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.1- <hash-algorithms-incompatible-with-php-7.1->`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `List Short Syntax <list-short-syntax>`{.interpreted-text
    role="ref"}
-   `List With Keys <list-with-keys>`{.interpreted-text role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `Malformed Octal <malformed-octal>`{.interpreted-text role="ref"}
-   `Multiple Definition Of The Same Argument <multiple-definition-of-the-same-argument>`{.interpreted-text
    role="ref"}
-   `Multiple Exceptions Catch() <multiple-exceptions-catch()>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 5.6 <new-functions-in-php-5.6>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.0 <new-functions-in-php-7.0>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No List With String <no-list-with-string>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No Return For Generator <no-return-for-generator>`{.interpreted-text
    role="ref"}
-   `No String With Append <no-string-with-append>`{.interpreted-text
    role="ref"}
-   `No Substr Minus One <no-substr-minus-one>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Null On New <null-on-new>`{.interpreted-text role="ref"}
-   `PHP 7.0 New Classes <php-7.0-new-classes>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 New Interfaces <php-7.0-new-interfaces>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Scalar Typehints <php-7.0-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Scalar Typehints <php-7.1-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `PHP5 Indirect Variable Expression <php5-indirect-variable-expression>`{.interpreted-text
    role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Parenthesis As Parameter <parenthesis-as-parameter>`{.interpreted-text
    role="ref"}
-   `Php 7 Indirect Expression <php-7-indirect-expression>`{.interpreted-text
    role="ref"}
-   `Php 7.1 New Class <php-7.1-new-class>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php7 Relaxed Keyword <php7-relaxed-keyword>`{.interpreted-text
    role="ref"}
-   `Switch With Too Many Default <switch-with-too-many-default>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Partial <unicode-escape-partial>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Syntax <unicode-escape-syntax>`{.interpreted-text
    role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use Const And Functions <use-const-and-functions>`{.interpreted-text
    role="ref"}
-   `Use Nullable Type <use-nullable-type>`{.interpreted-text
    role="ref"}
-   `Use password_hash() <use-password\_hash()>`{.interpreted-text
    role="ref"}
-   `Variable Global <variable-global>`{.interpreted-text role="ref"}
-   `__debugInfo() Usage <\_\_debuginfo()-usage>`{.interpreted-text
    role="ref"}
-   `ext/apc <ext/apc>`{.interpreted-text role="ref"}
-   `ext/mysql <ext/mysql>`{.interpreted-text role="ref"}
-   `isset() With Constant <isset()-with-constant>`{.interpreted-text
    role="ref"}

### CompatibilityPHP56

This ruleset centralizes all analysis for the migration from PHP 5.5 to
5.6.

Total : 57 analysis

-   `$HTTP_RAW_POST_DATA Usage <$http\_raw\_post\_data-usage>`{.interpreted-text
    role="ref"}
-   `Anonymous Classes <anonymous-classes>`{.interpreted-text
    role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Const Visibility Usage <const-visibility-usage>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Define With Array <define-with-array>`{.interpreted-text
    role="ref"}
-   `Direct Call To __clone() <direct-call-to-\_\_clone()>`{.interpreted-text
    role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Generator Cannot Return <generator-cannot-return>`{.interpreted-text
    role="ref"}
-   `Group Use Declaration <group-use-declaration>`{.interpreted-text
    role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.1- <hash-algorithms-incompatible-with-php-7.1->`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `List Short Syntax <list-short-syntax>`{.interpreted-text
    role="ref"}
-   `List With Keys <list-with-keys>`{.interpreted-text role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `Malformed Octal <malformed-octal>`{.interpreted-text role="ref"}
-   `Multiple Definition Of The Same Argument <multiple-definition-of-the-same-argument>`{.interpreted-text
    role="ref"}
-   `Multiple Exceptions Catch() <multiple-exceptions-catch()>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.0 <new-functions-in-php-7.0>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No List With String <no-list-with-string>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No Return For Generator <no-return-for-generator>`{.interpreted-text
    role="ref"}
-   `No String With Append <no-string-with-append>`{.interpreted-text
    role="ref"}
-   `No Substr Minus One <no-substr-minus-one>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `Non Static Methods Called In A Static <non-static-methods-called-in-a-static>`{.interpreted-text
    role="ref"}
-   `Null On New <null-on-new>`{.interpreted-text role="ref"}
-   `PHP 7.0 New Classes <php-7.0-new-classes>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 New Interfaces <php-7.0-new-interfaces>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Scalar Typehints <php-7.0-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Scalar Typehints <php-7.1-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `PHP5 Indirect Variable Expression <php5-indirect-variable-expression>`{.interpreted-text
    role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Parenthesis As Parameter <parenthesis-as-parameter>`{.interpreted-text
    role="ref"}
-   `Php 7 Indirect Expression <php-7-indirect-expression>`{.interpreted-text
    role="ref"}
-   `Php 7.1 New Class <php-7.1-new-class>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Php7 Relaxed Keyword <php7-relaxed-keyword>`{.interpreted-text
    role="ref"}
-   `Switch With Too Many Default <switch-with-too-many-default>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Partial <unicode-escape-partial>`{.interpreted-text
    role="ref"}
-   `Unicode Escape Syntax <unicode-escape-syntax>`{.interpreted-text
    role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use Nullable Type <use-nullable-type>`{.interpreted-text
    role="ref"}
-   `Variable Global <variable-global>`{.interpreted-text role="ref"}
-   `isset() With Constant <isset()-with-constant>`{.interpreted-text
    role="ref"}

### CompatibilityPHP70

This ruleset centralizes all analysis for the migration from PHP 5.6 to
7.0.

Total : 49 analysis

-   `Break Outside Loop <break-outside-loop>`{.interpreted-text
    role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Const Visibility Usage <const-visibility-usage>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Empty List <empty-list>`{.interpreted-text role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Foreach Don't Change Pointer <foreach-don't-change-pointer>`{.interpreted-text
    role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.1- <hash-algorithms-incompatible-with-php-7.1->`{.interpreted-text
    role="ref"}
-   `Hexadecimal In String <hexadecimal-in-string>`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `List Short Syntax <list-short-syntax>`{.interpreted-text
    role="ref"}
-   `List With Appends <list-with-appends>`{.interpreted-text
    role="ref"}
-   `List With Keys <list-with-keys>`{.interpreted-text role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `Magic Visibility <magic-visibility>`{.interpreted-text role="ref"}
-   `Multiple Exceptions Catch() <multiple-exceptions-catch()>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No Substr Minus One <no-substr-minus-one>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Removed Directives <php-7.0-removed-directives>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Removed Functions <php-7.0-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Scalar Typehints <php-7.1-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `Php 7 Indirect Expression <php-7-indirect-expression>`{.interpreted-text
    role="ref"}
-   `Php 7.1 New Class <php-7.1-new-class>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Reserved Keywords In PHP 7 <reserved-keywords-in-php-7>`{.interpreted-text
    role="ref"}
-   `Setlocale() Uses Constants <setlocale()-uses-constants>`{.interpreted-text
    role="ref"}
-   `Simple Global Variable <simple-global-variable>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Union Typehint <union-typehint>`{.interpreted-text role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use Nullable Type <use-nullable-type>`{.interpreted-text
    role="ref"}
-   `Usort Sorting In PHP 7.0 <usort-sorting-in-php-7.0>`{.interpreted-text
    role="ref"}
-   `ext/ereg <ext/ereg>`{.interpreted-text role="ref"}
-   `func_get_arg() Modified <func\_get\_arg()-modified>`{.interpreted-text
    role="ref"}
-   `mcrypt_create_iv() With Default Values <mcrypt\_create\_iv()-with-default-values>`{.interpreted-text
    role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}
-   `set_exception_handler() Warning <set\_exception\_handler()-warning>`{.interpreted-text
    role="ref"}

### CompatibilityPHP71

This ruleset centralizes all analysis for the migration from PHP 7.0 to
7.1.

Total : 36 analysis

-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Cant Inherit Abstract Method <cant-inherit-abstract-method>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Group Use Trailing Comma <group-use-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hexadecimal In String <hexadecimal-in-string>`{.interpreted-text
    role="ref"}
-   `Integer As Property <integer-as-property>`{.interpreted-text
    role="ref"}
-   `Invalid Octal In String <invalid-octal-in-string>`{.interpreted-text
    role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.1 <new-functions-in-php-7.1>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Removed Directives <php-7.0-removed-directives>`{.interpreted-text
    role="ref"}
-   `PHP 7.0 Removed Functions <php-7.0-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Microseconds <php-7.1-microseconds>`{.interpreted-text
    role="ref"}
-   `PHP 7.1 Removed Directives <php-7.1-removed-directives>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Scalar Typehints <php-7.2-scalar-typehints>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Signature Trailing Comma <signature-trailing-comma>`{.interpreted-text
    role="ref"}
-   `String Initialization <string-initialization>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Union Typehint <union-typehint>`{.interpreted-text role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `Use random_int() <use-random\_int()>`{.interpreted-text role="ref"}
-   `Using $this Outside A Class <using-$this-outside-a-class>`{.interpreted-text
    role="ref"}
-   `ext/mcrypt <ext/mcrypt>`{.interpreted-text role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}

### CompatibilityPHP72

This ruleset centralizes all analysis for the migration from PHP 7.1 to
7.2.

Total : 29 analysis

-   `Avoid set_error_handler $context Argument <avoid-set\_error\_handler-$context-argument>`{.interpreted-text
    role="ref"}
-   `Can't Count Non-Countable <can't-count-non-countable>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Flexible Heredoc <flexible-heredoc>`{.interpreted-text role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.3 <hash-algorithms-incompatible-with-php-5.3>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 5.4/5.5 <hash-algorithms-incompatible-with-php-5.4/5.5>`{.interpreted-text
    role="ref"}
-   `Hash Will Use Objects <hash-will-use-objects>`{.interpreted-text
    role="ref"}
-   `List With Reference <list-with-reference>`{.interpreted-text
    role="ref"}
-   `New Constants In PHP 7.2 <new-constants-in-php-7.2>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.2 <new-functions-in-php-7.2>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `No Reference For Static Property <no-reference-for-static-property>`{.interpreted-text
    role="ref"}
-   `No get_class() With Null <no-get\_class()-with-null>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Deprecations <php-7.2-deprecations>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Object Keyword <php-7.2-object-keyword>`{.interpreted-text
    role="ref"}
-   `PHP 7.2 Removed Functions <php-7.2-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Last Empty Argument <php-7.3-last-empty-argument>`{.interpreted-text
    role="ref"}
-   `Php 7.2 New Class <php-7.2-new-class>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Signature Trailing Comma <signature-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Throw Was An Expression <throw-was-an-expression>`{.interpreted-text
    role="ref"}
-   `Trailing Comma In Calls <trailing-comma-in-calls>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Undefined Constants <undefined-constants>`{.interpreted-text
    role="ref"}
-   `Union Typehint <union-typehint>`{.interpreted-text role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}

### CompatibilityPHP73

This ruleset centralizes all analysis for the migration from PHP 7.2 to
7.3.

Total : 18 analysis

-   `Assert Function Is Reserved <assert-function-is-reserved>`{.interpreted-text
    role="ref"}
-   `Case Insensitive Constants <case-insensitive-constants>`{.interpreted-text
    role="ref"}
-   `Coalesce Equal <coalesce-equal>`{.interpreted-text role="ref"}
-   `Compact Inexistant Variable <compact-inexistant-variable>`{.interpreted-text
    role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Continue Is For Loop <continue-is-for-loop>`{.interpreted-text
    role="ref"}
-   `Don't Read And Write In One Expression <don't-read-and-write-in-one-expression>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.3 <new-functions-in-php-7.3>`{.interpreted-text
    role="ref"}
-   `Numeric Literal Separator <numeric-literal-separator>`{.interpreted-text
    role="ref"}
-   `PHP 7.3 Removed Functions <php-7.3-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 74 New Directives <php-74-new-directives>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Signature Trailing Comma <signature-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Throw Was An Expression <throw-was-an-expression>`{.interpreted-text
    role="ref"}
-   `Typed Property Usage <typed-property-usage>`{.interpreted-text
    role="ref"}
-   `Union Typehint <union-typehint>`{.interpreted-text role="ref"}
-   `Unknown Pcre2 Option <unknown-pcre2-option>`{.interpreted-text
    role="ref"}
-   `Unpacking Inside Arrays <unpacking-inside-arrays>`{.interpreted-text
    role="ref"}

### CompatibilityPHP74

This ruleset centralizes all analysis for the migration from PHP 7.3 to
7.4.

Total : 29 analysis

-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Detect Current Class <detect-current-class>`{.interpreted-text
    role="ref"}
-   `Don't Read And Write In One Expression <don't-read-and-write-in-one-expression>`{.interpreted-text
    role="ref"}
-   `Filter To add_slashes() <filter-to-add\_slashes()>`{.interpreted-text
    role="ref"}
-   `Hash Algorithms Incompatible With PHP 7.4- <hash-algorithms-incompatible-with-php-7.4->`{.interpreted-text
    role="ref"}
-   `Nested Ternary Without Parenthesis <nested-ternary-without-parenthesis>`{.interpreted-text
    role="ref"}
-   `New Constants In PHP 7.4 <new-constants-in-php-7.4>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 7.4 <new-functions-in-php-7.4>`{.interpreted-text
    role="ref"}
-   `New Functions In PHP 8.0 <new-functions-in-php-8.0>`{.interpreted-text
    role="ref"}
-   `No More Curly Arrays <no-more-curly-arrays>`{.interpreted-text
    role="ref"}
-   `PHP 7.4 Constant Deprecation <php-7.4-constant-deprecation>`{.interpreted-text
    role="ref"}
-   `PHP 7.4 Removed Directives <php-7.4-removed-directives>`{.interpreted-text
    role="ref"}
-   `PHP 7.4 Removed Functions <php-7.4-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 7.4 Reserved Keyword <php-7.4-reserved-keyword>`{.interpreted-text
    role="ref"}
-   `Php 7.4 New Class <php-7.4-new-class>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Only TypeHints <php-8.0-only-typehints>`{.interpreted-text
    role="ref"}
-   `Php 8.0 Variable Syntax Tweaks <php-8.0-variable-syntax-tweaks>`{.interpreted-text
    role="ref"}
-   `Php/UseMatch <php/usematch>`{.interpreted-text role="ref"}
-   `Reflection Export() Is Deprecated <reflection-export()-is-deprecated>`{.interpreted-text
    role="ref"}
-   `Scalar Are Not Arrays <scalar-are-not-arrays>`{.interpreted-text
    role="ref"}
-   `Signature Trailing Comma <signature-trailing-comma>`{.interpreted-text
    role="ref"}
-   `Throw Was An Expression <throw-was-an-expression>`{.interpreted-text
    role="ref"}
-   `Unbinding Closures <unbinding-closures>`{.interpreted-text
    role="ref"}
-   `Union Typehint <union-typehint>`{.interpreted-text role="ref"}
-   `array_key_exists() Works On Arrays <array\_key\_exists()-works-on-arrays>`{.interpreted-text
    role="ref"}
-   `curl_version() Has No Argument <curl\_version()-has-no-argument>`{.interpreted-text
    role="ref"}
-   `idn_to_ascii() New Default <idn\_to\_ascii()-new-default>`{.interpreted-text
    role="ref"}
-   `mb_strrpos() Third Argument <mb\_strrpos()-third-argument>`{.interpreted-text
    role="ref"}
-   `openssl_random_pseudo_byte() Second Argument <openssl\_random\_pseudo\_byte()-second-argument>`{.interpreted-text
    role="ref"}

### CompatibilityPHP80

This ruleset centralizes all analysis for the migration from PHP 7.4 to
8.0.

Total : 13 analysis

-   `$php_errormsg Usage <$php\_errormsg-usage>`{.interpreted-text
    role="ref"}
-   `Cast Unset Usage <cast-unset-usage>`{.interpreted-text role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Mismatch Parameter Name <mismatch-parameter-name>`{.interpreted-text
    role="ref"}
-   `Negative Start Index In Array <negative-start-index-in-array>`{.interpreted-text
    role="ref"}
-   `Nullable With Constant <nullable-with-constant>`{.interpreted-text
    role="ref"}
-   `Old Style Constructor <old-style-constructor>`{.interpreted-text
    role="ref"}
-   `PHP 8.0 Removed Constants <php-8.0-removed-constants>`{.interpreted-text
    role="ref"}
-   `PHP 8.0 Removed Directives <php-8.0-removed-directives>`{.interpreted-text
    role="ref"}
-   `PHP 8.0 Removed Functions <php-8.0-removed-functions>`{.interpreted-text
    role="ref"}
-   `PHP 80 Named Parameter Variadic <php-80-named-parameter-variadic>`{.interpreted-text
    role="ref"}
-   `PHP Resources Turned Into Objects <php-resources-turned-into-objects>`{.interpreted-text
    role="ref"}
-   `Unsupported Types With Operators <unsupported-types-with-operators>`{.interpreted-text
    role="ref"}

### Dead code

This ruleset focuses on dead code : expressions or even structures that
are written, valid but never used.

Total : 26 analysis

-   `Can't Extend Final <can't-extend-final>`{.interpreted-text
    role="ref"}
-   `Empty Instructions <empty-instructions>`{.interpreted-text
    role="ref"}
-   `Empty Namespace <empty-namespace>`{.interpreted-text role="ref"}
-   `Exception Order <exception-order>`{.interpreted-text role="ref"}
-   `Locally Unused Property <locally-unused-property>`{.interpreted-text
    role="ref"}
-   `Rethrown Exceptions <rethrown-exceptions>`{.interpreted-text
    role="ref"}
-   `Self Using Trait <self-using-trait>`{.interpreted-text role="ref"}
-   `Undefined Caught Exceptions <undefined-caught-exceptions>`{.interpreted-text
    role="ref"}
-   `Unreachable Code <unreachable-code>`{.interpreted-text role="ref"}
-   `Unresolved Catch <unresolved-catch>`{.interpreted-text role="ref"}
-   `Unresolved Instanceof <unresolved-instanceof>`{.interpreted-text
    role="ref"}
-   `Unset In Foreach <unset-in-foreach>`{.interpreted-text role="ref"}
-   `Unthrown Exception <unthrown-exception>`{.interpreted-text
    role="ref"}
-   `Unused Classes <unused-classes>`{.interpreted-text role="ref"}
-   `Unused Constants <unused-constants>`{.interpreted-text role="ref"}
-   `Unused Functions <unused-functions>`{.interpreted-text role="ref"}
-   `Unused Inherited Variable In Closure <unused-inherited-variable-in-closure>`{.interpreted-text
    role="ref"}
-   `Unused Interfaces <unused-interfaces>`{.interpreted-text
    role="ref"}
-   `Unused Label <unused-label>`{.interpreted-text role="ref"}
-   `Unused Methods <unused-methods>`{.interpreted-text role="ref"}
-   `Unused Private Methods <unused-private-methods>`{.interpreted-text
    role="ref"}
-   `Unused Private Properties <unused-private-properties>`{.interpreted-text
    role="ref"}
-   `Unused Protected Methods <unused-protected-methods>`{.interpreted-text
    role="ref"}
-   `Unused Returned Value <unused-returned-value>`{.interpreted-text
    role="ref"}
-   `Unused Use <unused-use>`{.interpreted-text role="ref"}
-   `Useless Type Check <useless-type-check>`{.interpreted-text
    role="ref"}

### LintButWontExec

This ruleset focuses on PHP code that lint (php -l), but that will not
run. As such, this ruleset tries to go further than PHP, by connecting
files, just like during execution.

Total : 29 analysis

-   `Abstract Or Implements <abstract-or-implements>`{.interpreted-text
    role="ref"}
-   `Can't Throw Throwable <can't-throw-throwable>`{.interpreted-text
    role="ref"}
-   `Cant Implement Traversable <cant-implement-traversable>`{.interpreted-text
    role="ref"}
-   `Classes Mutually Extending Each Other <classes-mutually-extending-each-other>`{.interpreted-text
    role="ref"}
-   `Clone With Non-Object <clone-with-non-object>`{.interpreted-text
    role="ref"}
-   `Concrete Visibility <concrete-visibility>`{.interpreted-text
    role="ref"}
-   `Could Be Stringable <could-be-stringable>`{.interpreted-text
    role="ref"}
-   `Final Class Usage <final-class-usage>`{.interpreted-text
    role="ref"}
-   `Final Methods Usage <final-methods-usage>`{.interpreted-text
    role="ref"}
-   `Incompatible Signature Methods <incompatible-signature-methods>`{.interpreted-text
    role="ref"}
-   `Interfaces Is Not Implemented <interfaces-is-not-implemented>`{.interpreted-text
    role="ref"}
-   `Method Collision Traits <method-collision-traits>`{.interpreted-text
    role="ref"}
-   `Method Signature Must Be Compatible <method-signature-must-be-compatible>`{.interpreted-text
    role="ref"}
-   `Mismatch Properties Typehints <mismatch-properties-typehints>`{.interpreted-text
    role="ref"}
-   `Mismatch Type And Default <mismatch-type-and-default>`{.interpreted-text
    role="ref"}
-   `Must Return Methods <must-return-methods>`{.interpreted-text
    role="ref"}
-   `No Magic Method With Array <no-magic-method-with-array>`{.interpreted-text
    role="ref"}
-   `No Self Referencing Constant <no-self-referencing-constant>`{.interpreted-text
    role="ref"}
-   `Only Variable For Reference <only-variable-for-reference>`{.interpreted-text
    role="ref"}
-   `Raised Access Level <raised-access-level>`{.interpreted-text
    role="ref"}
-   `Repeated Interface <repeated-interface>`{.interpreted-text
    role="ref"}
-   `Trait Not Found <trait-not-found>`{.interpreted-text role="ref"}
-   `Typehint Must Be Returned <typehint-must-be-returned>`{.interpreted-text
    role="ref"}
-   `Undefined Insteadof <undefined-insteadof>`{.interpreted-text
    role="ref"}
-   `Undefined Trait <undefined-trait>`{.interpreted-text role="ref"}
-   `Useless Alias <useless-alias>`{.interpreted-text role="ref"}
-   `Using $this Outside A Class <using-$this-outside-a-class>`{.interpreted-text
    role="ref"}
-   `Wrong Typed Property Default <wrong-typed-property-default>`{.interpreted-text
    role="ref"}
-   `self, parent, static Outside Class <self,-parent,-static-outside-class>`{.interpreted-text
    role="ref"}

### Performances

This ruleset focuses on performances issues : anything that slows the
code\'s execution.

Total : 46 analysis

-   `@ Operator <@-operator>`{.interpreted-text role="ref"}
-   `Always Use Function With array_key_exists() <always-use-function-with-array\_key\_exists()>`{.interpreted-text
    role="ref"}
-   `Autoappend <autoappend>`{.interpreted-text role="ref"}
-   `Avoid Concat In Loop <avoid-concat-in-loop>`{.interpreted-text
    role="ref"}
-   `Avoid Large Array Assignation <avoid-large-array-assignation>`{.interpreted-text
    role="ref"}
-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Avoid array_push() <avoid-array\_push()>`{.interpreted-text
    role="ref"}
-   `Avoid array_unique() <avoid-array\_unique()>`{.interpreted-text
    role="ref"}
-   `Avoid glob() Usage <avoid-glob()-usage>`{.interpreted-text
    role="ref"}
-   `Cache Variable Outside Loop <cache-variable-outside-loop>`{.interpreted-text
    role="ref"}
-   `Closure Could Be A Callback <closure-could-be-a-callback>`{.interpreted-text
    role="ref"}
-   `Could Use Short Assignation <could-use-short-assignation>`{.interpreted-text
    role="ref"}
-   `Do In Base <do-in-base>`{.interpreted-text role="ref"}
-   `Double array_flip() <double-array\_flip()>`{.interpreted-text
    role="ref"}
-   `Echo With Concat <echo-with-concat>`{.interpreted-text role="ref"}
-   `Eval() Usage <eval()-usage>`{.interpreted-text role="ref"}
-   `Fetch One Row Format <fetch-one-row-format>`{.interpreted-text
    role="ref"}
-   `For Using Functioncall <for-using-functioncall>`{.interpreted-text
    role="ref"}
-   `Getting Last Element <getting-last-element>`{.interpreted-text
    role="ref"}
-   `Global Inside Loop <global-inside-loop>`{.interpreted-text
    role="ref"}
-   `Isset() On The Whole Array <isset()-on-the-whole-array>`{.interpreted-text
    role="ref"}
-   `Joining file() <joining-file()>`{.interpreted-text role="ref"}
-   `Make Magic Concrete <make-magic-concrete>`{.interpreted-text
    role="ref"}
-   `Make One Call With Array <make-one-call-with-array>`{.interpreted-text
    role="ref"}
-   `No Count With 0 <no-count-with-0>`{.interpreted-text role="ref"}
-   `No array_merge() In Loops <no-array\_merge()-in-loops>`{.interpreted-text
    role="ref"}
-   `No mb_substr In Loop <no-mb\_substr-in-loop>`{.interpreted-text
    role="ref"}
-   `Optimize Explode() <optimize-explode()>`{.interpreted-text
    role="ref"}
-   `Pre-increment <pre-increment>`{.interpreted-text role="ref"}
-   `Processing Collector <processing-collector>`{.interpreted-text
    role="ref"}
-   `Regex On Arrays <regex-on-arrays>`{.interpreted-text role="ref"}
-   `Should Use Function <should-use-function>`{.interpreted-text
    role="ref"}
-   `Should Use array_column() <should-use-array\_column()>`{.interpreted-text
    role="ref"}
-   `Simple Switch <simple-switch>`{.interpreted-text role="ref"}
-   `Simplify Regex <simplify-regex>`{.interpreted-text role="ref"}
-   `Slice Arrays First <slice-arrays-first>`{.interpreted-text
    role="ref"}
-   `Slow Functions <slow-functions>`{.interpreted-text role="ref"}
-   `Substring First <substring-first>`{.interpreted-text role="ref"}
-   `Use PHP7 Encapsed Strings <use-php7-encapsed-strings>`{.interpreted-text
    role="ref"}
-   `Use The Blind Var <use-the-blind-var>`{.interpreted-text
    role="ref"}
-   `Use \:\:Class Operator <use-\:\:class-operator>`{.interpreted-text
    role="ref"}
-   `Use pathinfo() Arguments <use-pathinfo()-arguments>`{.interpreted-text
    role="ref"}
-   `While(List() = Each()) <while(list()-=-each())>`{.interpreted-text
    role="ref"}
-   `array_key_exists() Speedup <array\_key\_exists()-speedup>`{.interpreted-text
    role="ref"}
-   `fputcsv() In Loops <fputcsv()-in-loops>`{.interpreted-text
    role="ref"}
-   `time() Vs strtotime() <time()-vs-strtotime()>`{.interpreted-text
    role="ref"}

### Rector

[RectorPHP](https://getrector.org/) is a reconstructor tool. It applies
modifications in the PHP code automatically. Exakat finds results which
may be automatically updated with rector.

Total : 3 analysis

-   `Else If Versus Elseif <else-if-versus-elseif>`{.interpreted-text
    role="ref"}
-   `Is_A() With String <is\_a()-with-string>`{.interpreted-text
    role="ref"}
-   `Preprocessable <preprocessable>`{.interpreted-text role="ref"}

### Security

This ruleset focuses on code security.

Total : 44 analysis

-   `Always Anchor Regex <always-anchor-regex>`{.interpreted-text
    role="ref"}
-   `Avoid Those Hash Functions <avoid-those-hash-functions>`{.interpreted-text
    role="ref"}
-   `Avoid sleep()/usleep() <avoid-sleep()/usleep()>`{.interpreted-text
    role="ref"}
-   `Check Crypto Key Length <check-crypto-key-length>`{.interpreted-text
    role="ref"}
-   `Compare Hash <compare-hash>`{.interpreted-text role="ref"}
-   `Configure Extract <configure-extract>`{.interpreted-text
    role="ref"}
-   `Direct Injection <direct-injection>`{.interpreted-text role="ref"}
-   `Don't Echo Error <don't-echo-error>`{.interpreted-text role="ref"}
-   `Dynamic Library Loading <dynamic-library-loading>`{.interpreted-text
    role="ref"}
-   `Encoded Simple Letters <encoded-simple-letters>`{.interpreted-text
    role="ref"}
-   `Eval() Usage <eval()-usage>`{.interpreted-text role="ref"}
-   `Hardcoded Passwords <hardcoded-passwords>`{.interpreted-text
    role="ref"}
-   `Indirect Injection <indirect-injection>`{.interpreted-text
    role="ref"}
-   `Integer Conversion <integer-conversion>`{.interpreted-text
    role="ref"}
-   `Keep Files Access Restricted <keep-files-access-restricted>`{.interpreted-text
    role="ref"}
-   `Minus One On Error <minus-one-on-error>`{.interpreted-text
    role="ref"}
-   `Mkdir Default <mkdir-default>`{.interpreted-text role="ref"}
-   `No ENT_IGNORE <no-ent\_ignore>`{.interpreted-text role="ref"}
-   `No Hardcoded Hash <no-hardcoded-hash>`{.interpreted-text
    role="ref"}
-   `No Hardcoded Ip <no-hardcoded-ip>`{.interpreted-text role="ref"}
-   `No Hardcoded Port <no-hardcoded-port>`{.interpreted-text
    role="ref"}
-   `No Net For Xml Load <no-net-for-xml-load>`{.interpreted-text
    role="ref"}
-   `No Return Or Throw In Finally <no-return-or-throw-in-finally>`{.interpreted-text
    role="ref"}
-   `No Weak SSL Crypto <no-weak-ssl-crypto>`{.interpreted-text
    role="ref"}
-   `Phpinfo <phpinfo>`{.interpreted-text role="ref"}
-   `Random Without Try <random-without-try>`{.interpreted-text
    role="ref"}
-   `Register Globals <register-globals>`{.interpreted-text role="ref"}
-   `Safe Curl Options <safe-curl-options>`{.interpreted-text
    role="ref"}
-   `Safe HTTP Headers <safe-http-headers>`{.interpreted-text
    role="ref"}
-   `Session Lazy Write <session-lazy-write>`{.interpreted-text
    role="ref"}
-   `Set Cookie Safe Arguments <set-cookie-safe-arguments>`{.interpreted-text
    role="ref"}
-   `Should Use Prepared Statement <should-use-prepared-statement>`{.interpreted-text
    role="ref"}
-   `Should Use session_regenerateid() <should-use-session\_regenerateid()>`{.interpreted-text
    role="ref"}
-   `Sqlite3 Requires Single Quotes <sqlite3-requires-single-quotes>`{.interpreted-text
    role="ref"}
-   `Switch Fallthrough <switch-fallthrough>`{.interpreted-text
    role="ref"}
-   `Unserialize Second Arg <unserialize-second-arg>`{.interpreted-text
    role="ref"}
-   `Upload Filename Injection <upload-filename-injection>`{.interpreted-text
    role="ref"}
-   `Use random_int() <use-random\_int()>`{.interpreted-text role="ref"}
-   `eval() Without Try <eval()-without-try>`{.interpreted-text
    role="ref"}
-   `filter_input() As A Source <filter\_input()-as-a-source>`{.interpreted-text
    role="ref"}
-   `move_uploaded_file Instead Of copy <move\_uploaded\_file-instead-of-copy>`{.interpreted-text
    role="ref"}
-   `parse_str() Warning <parse\_str()-warning>`{.interpreted-text
    role="ref"}
-   `preg_replace With Option e <preg\_replace-with-option-e>`{.interpreted-text
    role="ref"}
-   `var_dump()... Usage <var\_dump()...-usage>`{.interpreted-text
    role="ref"}

### Semantics

This ruleset focuses on human interpretation of the code. It reviews
special values of literals, and named structures.

Total : 13 analysis

-   `Class Function Confusion <class-function-confusion>`{.interpreted-text
    role="ref"}
-   `Duplicate Literal <duplicate-literal>`{.interpreted-text
    role="ref"}
-   `Fn Argument Variable Confusion <fn-argument-variable-confusion>`{.interpreted-text
    role="ref"}
-   `Mismatch Parameter And Type <mismatch-parameter-and-type>`{.interpreted-text
    role="ref"}
-   `One Letter Functions <one-letter-functions>`{.interpreted-text
    role="ref"}
-   `Parameter Hiding <parameter-hiding>`{.interpreted-text role="ref"}
-   `Prefix And Suffixes With Typehint <prefix-and-suffixes-with-typehint>`{.interpreted-text
    role="ref"}
-   `Property Variable Confusion <property-variable-confusion>`{.interpreted-text
    role="ref"}
-   `Semantic Typing <semantic-typing>`{.interpreted-text role="ref"}
-   `Similar Integers <similar-integers>`{.interpreted-text role="ref"}
-   `Variables With One Letter Names <variables-with-one-letter-names>`{.interpreted-text
    role="ref"}
-   `Weird Array Index <weird-array-index>`{.interpreted-text
    role="ref"}
-   `Wrong Typehinted Name <wrong-typehinted-name>`{.interpreted-text
    role="ref"}

### Suggestions

This ruleset focuses on possibly better syntax than the one currently
used. Those may be code modernization, alternatives, more efficient
solutions, or simply left over from older versions.

Total : 95 analysis

-   `** For Exponent <**-for-exponent>`{.interpreted-text role="ref"}
-   `Abstract Away <abstract-away>`{.interpreted-text role="ref"}
-   `Add Default Value <add-default-value>`{.interpreted-text
    role="ref"}
-   `Already Parents Interface <already-parents-interface>`{.interpreted-text
    role="ref"}
-   `Avoid Real <avoid-real>`{.interpreted-text role="ref"}
-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Cancel Common Method <cancel-common-method>`{.interpreted-text
    role="ref"}
-   `Closure Could Be A Callback <closure-could-be-a-callback>`{.interpreted-text
    role="ref"}
-   `Compact Inexistant Variable <compact-inexistant-variable>`{.interpreted-text
    role="ref"}
-   `Complex Dynamic Names <complex-dynamic-names>`{.interpreted-text
    role="ref"}
-   `Could Be Constant <could-be-constant>`{.interpreted-text
    role="ref"}
-   `Could Be Static Closure <could-be-static-closure>`{.interpreted-text
    role="ref"}
-   `Could Make A Function <could-make-a-function>`{.interpreted-text
    role="ref"}
-   `Could Use Alias <could-use-alias>`{.interpreted-text role="ref"}
-   `Could Use Compact <could-use-compact>`{.interpreted-text
    role="ref"}
-   `Could Use Promoted Properties <could-use-promoted-properties>`{.interpreted-text
    role="ref"}
-   `Could Use Try <could-use-try>`{.interpreted-text role="ref"}
-   `Could Use __DIR__ <could-use-\_\_dir\_\_>`{.interpreted-text
    role="ref"}
-   `Could Use array_fill_keys <could-use-array\_fill\_keys>`{.interpreted-text
    role="ref"}
-   `Could Use array_unique <could-use-array\_unique>`{.interpreted-text
    role="ref"}
-   `Could Use self <could-use-self>`{.interpreted-text role="ref"}
-   `Detect Current Class <detect-current-class>`{.interpreted-text
    role="ref"}
-   `Directly Use File <directly-use-file>`{.interpreted-text
    role="ref"}
-   `Don't Loop On Yield <don't-loop-on-yield>`{.interpreted-text
    role="ref"}
-   `Dont Compare Typed Boolean <dont-compare-typed-boolean>`{.interpreted-text
    role="ref"}
-   `Drop Else After Return <drop-else-after-return>`{.interpreted-text
    role="ref"}
-   `Drop Substr Last Arg <drop-substr-last-arg>`{.interpreted-text
    role="ref"}
-   `Echo With Concat <echo-with-concat>`{.interpreted-text role="ref"}
-   `Empty With Expression <empty-with-expression>`{.interpreted-text
    role="ref"}
-   `Function Subscripting, Old Style <function-subscripting,-old-style>`{.interpreted-text
    role="ref"}
-   `Implode One Arg <implode-one-arg>`{.interpreted-text role="ref"}
-   `Isset Multiple Arguments <isset-multiple-arguments>`{.interpreted-text
    role="ref"}
-   `Isset() On The Whole Array <isset()-on-the-whole-array>`{.interpreted-text
    role="ref"}
-   `Large Try Block <large-try-block>`{.interpreted-text role="ref"}
-   `Logical Should Use Symbolic Operators <logical-should-use-symbolic-operators>`{.interpreted-text
    role="ref"}
-   `Mismatched Ternary Alternatives <mismatched-ternary-alternatives>`{.interpreted-text
    role="ref"}
-   `Multiple Unset() <multiple-unset()>`{.interpreted-text role="ref"}
-   `Multiple Usage Of Same Trait <multiple-usage-of-same-trait>`{.interpreted-text
    role="ref"}
-   `Named Regex <named-regex>`{.interpreted-text role="ref"}
-   `Never Used Parameter <never-used-parameter>`{.interpreted-text
    role="ref"}
-   `No Need For get_class() <no-need-for-get\_class()>`{.interpreted-text
    role="ref"}
-   `No Parenthesis For Language Construct <no-parenthesis-for-language-construct>`{.interpreted-text
    role="ref"}
-   `No Return Used <no-return-used>`{.interpreted-text role="ref"}
-   `One If Is Sufficient <one-if-is-sufficient>`{.interpreted-text
    role="ref"}
-   `Overwritten Exceptions <overwritten-exceptions>`{.interpreted-text
    role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Parent First <parent-first>`{.interpreted-text role="ref"}
-   `Possible Alias Confusion <possible-alias-confusion>`{.interpreted-text
    role="ref"}
-   `Possible Increment <possible-increment>`{.interpreted-text
    role="ref"}
-   `Preprocess Arrays <preprocess-arrays>`{.interpreted-text
    role="ref"}
-   `Randomly Sorted Arrays <randomly-sorted-arrays>`{.interpreted-text
    role="ref"}
-   `Repeated print() <repeated-print()>`{.interpreted-text role="ref"}
-   `Return With Parenthesis <return-with-parenthesis>`{.interpreted-text
    role="ref"}
-   `Reuse Variable <reuse-variable>`{.interpreted-text role="ref"}
-   `Set Aside Code <set-aside-code>`{.interpreted-text role="ref"}
-   `Should Deep Clone <should-deep-clone>`{.interpreted-text
    role="ref"}
-   `Should Have Destructor <should-have-destructor>`{.interpreted-text
    role="ref"}
-   `Should Preprocess Chr() <should-preprocess-chr()>`{.interpreted-text
    role="ref"}
-   `Should Use Coalesce <should-use-coalesce>`{.interpreted-text
    role="ref"}
-   `Should Use Foreach <should-use-foreach>`{.interpreted-text
    role="ref"}
-   `Should Use Math <should-use-math>`{.interpreted-text role="ref"}
-   `Should Use Operator <should-use-operator>`{.interpreted-text
    role="ref"}
-   `Should Use array_column() <should-use-array\_column()>`{.interpreted-text
    role="ref"}
-   `Should Use array_filter() <should-use-array\_filter()>`{.interpreted-text
    role="ref"}
-   `Slice Arrays First <slice-arrays-first>`{.interpreted-text
    role="ref"}
-   `Static Global Variables Confusion <static-global-variables-confusion>`{.interpreted-text
    role="ref"}
-   `Strict Comparison With Booleans <strict-comparison-with-booleans>`{.interpreted-text
    role="ref"}
-   `Substr To Trim <substr-to-trim>`{.interpreted-text role="ref"}
-   `Substring First <substring-first>`{.interpreted-text role="ref"}
-   `Too Long A Block <too-long-a-block>`{.interpreted-text role="ref"}
-   `Too Many Children <too-many-children>`{.interpreted-text
    role="ref"}
-   `Too Many Parameters <too-many-parameters>`{.interpreted-text
    role="ref"}
-   `Too Much Indented <too-much-indented>`{.interpreted-text
    role="ref"}
-   `Unitialized Properties <unitialized-properties>`{.interpreted-text
    role="ref"}
-   `Unreachable Code <unreachable-code>`{.interpreted-text role="ref"}
-   `Unused Exception Variable <unused-exception-variable>`{.interpreted-text
    role="ref"}
-   `Unused Interfaces <unused-interfaces>`{.interpreted-text
    role="ref"}
-   `Use Array Functions <use-array-functions>`{.interpreted-text
    role="ref"}
-   `Use Basename Suffix <use-basename-suffix>`{.interpreted-text
    role="ref"}
-   `Use Case Value <use-case-value>`{.interpreted-text role="ref"}
-   `Use Count Recursive <use-count-recursive>`{.interpreted-text
    role="ref"}
-   `Use DateTimeImmutable Class <use-datetimeimmutable-class>`{.interpreted-text
    role="ref"}
-   `Use List With Foreach <use-list-with-foreach>`{.interpreted-text
    role="ref"}
-   `Use Url Query Functions <use-url-query-functions>`{.interpreted-text
    role="ref"}
-   `Use get_debug_type() <use-get\_debug\_type()>`{.interpreted-text
    role="ref"}
-   `Use is_countable <use-is\_countable>`{.interpreted-text role="ref"}
-   `Use json_decode() Options <use-json\_decode()-options>`{.interpreted-text
    role="ref"}
-   `Use session_start() Options <use-session\_start()-options>`{.interpreted-text
    role="ref"}
-   `Use str_contains() <use-str\_contains()>`{.interpreted-text
    role="ref"}
-   `Useless Default Argument <useless-default-argument>`{.interpreted-text
    role="ref"}
-   `Useless Typehint <useless-typehint>`{.interpreted-text role="ref"}
-   `While(List() = Each()) <while(list()-=-each())>`{.interpreted-text
    role="ref"}
-   `array_key_exists() Speedup <array\_key\_exists()-speedup>`{.interpreted-text
    role="ref"}
-   `list() May Omit Variables <list()-may-omit-variables>`{.interpreted-text
    role="ref"}
-   `preg_match_all() Flag <preg\_match\_all()-flag>`{.interpreted-text
    role="ref"}

### Top10

This ruleset is a selection of analysis, with the top 10 most common.
Actually, it is a little larger than that.

Total : 28 analysis

-   `Avoid Concat In Loop <avoid-concat-in-loop>`{.interpreted-text
    role="ref"}
-   `Avoid Real <avoid-real>`{.interpreted-text role="ref"}
-   `Avoid Substr() One <avoid-substr()-one>`{.interpreted-text
    role="ref"}
-   `Concat And Addition <concat-and-addition>`{.interpreted-text
    role="ref"}
-   `Could Use str_repeat() <could-use-str\_repeat()>`{.interpreted-text
    role="ref"}
-   `Dangling Array References <dangling-array-references>`{.interpreted-text
    role="ref"}
-   `Don't Unset Properties <don't-unset-properties>`{.interpreted-text
    role="ref"}
-   `Failed Substr Comparison <failed-substr-comparison>`{.interpreted-text
    role="ref"}
-   `For Using Functioncall <for-using-functioncall>`{.interpreted-text
    role="ref"}
-   `Logical Operators Favorite <logical-operators-favorite>`{.interpreted-text
    role="ref"}
-   `Logical Should Use Symbolic Operators <logical-should-use-symbolic-operators>`{.interpreted-text
    role="ref"}
-   `Next Month Trap <next-month-trap>`{.interpreted-text role="ref"}
-   `No Choice <no-choice>`{.interpreted-text role="ref"}
-   `No Real Comparison <no-real-comparison>`{.interpreted-text
    role="ref"}
-   `No array_merge() In Loops <no-array\_merge()-in-loops>`{.interpreted-text
    role="ref"}
-   `Objects Don't Need References <objects-don't-need-references>`{.interpreted-text
    role="ref"}
-   `Possible Missing Subpattern <possible-missing-subpattern>`{.interpreted-text
    role="ref"}
-   `Queries In Loops <queries-in-loops>`{.interpreted-text role="ref"}
-   `Repeated print() <repeated-print()>`{.interpreted-text role="ref"}
-   `Should Yield With Key <should-yield-with-key>`{.interpreted-text
    role="ref"}
-   `Strpos()-like Comparison <strpos()-like-comparison>`{.interpreted-text
    role="ref"}
-   `Substring First <substring-first>`{.interpreted-text role="ref"}
-   `Unitialized Properties <unitialized-properties>`{.interpreted-text
    role="ref"}
-   `Unresolved Instanceof <unresolved-instanceof>`{.interpreted-text
    role="ref"}
-   `Use List With Foreach <use-list-with-foreach>`{.interpreted-text
    role="ref"}
-   `Use const <use-const>`{.interpreted-text role="ref"}
-   `Used Once Variables <used-once-variables>`{.interpreted-text
    role="ref"}
-   `fputcsv() In Loops <fputcsv()-in-loops>`{.interpreted-text
    role="ref"}

### Typechecks

This ruleset focuses on typehinting. Missing typehint, or inconsistent
typehint, are reported.

Total : 23 analysis

-   `Argument Should Be Typehinted <argument-should-be-typehinted>`{.interpreted-text
    role="ref"}
-   `Bad Typehint Relay <bad-typehint-relay>`{.interpreted-text
    role="ref"}
-   `Child Class Removes Typehint <child-class-removes-typehint>`{.interpreted-text
    role="ref"}
-   `Could Be Callable <could-be-callable>`{.interpreted-text
    role="ref"}
-   `Could Be Float <could-be-float>`{.interpreted-text role="ref"}
-   `Could Be Integer <could-be-integer>`{.interpreted-text role="ref"}
-   `Could Be Iterable <could-be-iterable>`{.interpreted-text
    role="ref"}
-   `Could Be Null <could-be-null>`{.interpreted-text role="ref"}
-   `Could Be Parent <could-be-parent>`{.interpreted-text role="ref"}
-   `Could Be Self <could-be-self>`{.interpreted-text role="ref"}
-   `Could Be String <could-be-string>`{.interpreted-text role="ref"}
-   `Could Be Void <could-be-void>`{.interpreted-text role="ref"}
-   `Fossilized Method <fossilized-method>`{.interpreted-text
    role="ref"}
-   `Insufficient Typehint <insufficient-typehint>`{.interpreted-text
    role="ref"}
-   `Mismatch Type And Default <mismatch-type-and-default>`{.interpreted-text
    role="ref"}
-   `Mismatched Default Arguments <mismatched-default-arguments>`{.interpreted-text
    role="ref"}
-   `Mismatched Typehint <mismatched-typehint>`{.interpreted-text
    role="ref"}
-   `Missing Typehint <missing-typehint>`{.interpreted-text role="ref"}
-   `No Class As Typehint <no-class-as-typehint>`{.interpreted-text
    role="ref"}
-   `Not A Scalar Type <not-a-scalar-type>`{.interpreted-text
    role="ref"}
-   `Useless Interfaces <useless-interfaces>`{.interpreted-text
    role="ref"}
-   `Wrong Argument Type <wrong-argument-type>`{.interpreted-text
    role="ref"}
-   `Wrong Type With Call <wrong-type-with-call>`{.interpreted-text
    role="ref"}

### php-cs-fixable

\[PHP-CS-fixer\](<https://github.com/FriendsOfPHP/PHP-CS-Fixer>) is a
tool to automatically fix PHP Coding Standards issues. It applies
modifications in the PHP code automatically. Exakat finds results which
may be automatically updated with php-cs-fixer.

Total : 11 analysis

-   `** For Exponent <**-for-exponent>`{.interpreted-text role="ref"}
-   `Could Use __DIR__ <could-use-\_\_dir\_\_>`{.interpreted-text
    role="ref"}
-   `Don't Unset Properties <don't-unset-properties>`{.interpreted-text
    role="ref"}
-   `Else If Versus Elseif <else-if-versus-elseif>`{.interpreted-text
    role="ref"}
-   `Implode One Arg <implode-one-arg>`{.interpreted-text role="ref"}
-   `Isset Multiple Arguments <isset-multiple-arguments>`{.interpreted-text
    role="ref"}
-   `Logical Should Use Symbolic Operators <logical-should-use-symbolic-operators>`{.interpreted-text
    role="ref"}
-   `Multiple Unset() <multiple-unset()>`{.interpreted-text role="ref"}
-   `PHP7 Dirname <php7-dirname>`{.interpreted-text role="ref"}
-   `Use === null <use-===-null>`{.interpreted-text role="ref"}
-   `Use Constant <use-constant>`{.interpreted-text role="ref"}
