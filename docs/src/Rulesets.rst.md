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
