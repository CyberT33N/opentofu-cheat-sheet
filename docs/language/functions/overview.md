# Functions

[INTENT: NAVIGATION]

The OpenTofu language includes built-in functions that can be called from within expressions to transform and combine values. The general syntax for function calls is a function name followed by comma-separated arguments in parentheses: `max(5, 12, 9)`.

The catalog below is the complete built-in function surface of the locally installed OpenTofu v1.12.5, sourced from the programmatic surface [`tofu metadata functions -json`](../../cli/metadata/functions/overview.md) and cross-checked against the [official function documentation](https://opentofu.org/docs/language/functions/). Every function is additionally addressable under its `core::` namespaced alias (for example `core::abs`).

Any function can be probed live from the expression console: `echo 'max(5, 12, 9)' | tofu console` prints `12` (verified locally; see [cli/console](../../cli/console/overview.md)).

## Provider-defined functions

As of OpenTofu 1.7.0, providers may define their own functions, available during execution under `provider::<provider_name>::<function_name>` (with aliases: `provider::<provider_name>::<provider_alias>::<function_name>`). Functions are scoped to the module that requires the provider and are not inherited by child modules. The [built-in provider](../providers/builtin.md) `terraform.io/builtin/terraform` registers three provider-defined functions (verified through [`tofu providers schema -json`](../../cli/providers/schema/overview.md)): `provider::terraform::decode_tfvars`, `provider::terraform::encode_expr`, and `provider::terraform::encode_tfvars`.

The official documentation additionally carries concept pages for provider-defined function families (`assume_family`, `convert`, `type`); these are not built-in functions of the installed version and are therefore not part of this catalog.

## Function catalog (121 built-in functions)

- [abs](abs.md) — absolute value of a number
- [abspath](abspath.md) — convert a path to an absolute path
- [alltrue](alltrue.md) — `true` if all elements are `true`
- [anytrue](anytrue.md) — `true` if any element is `true`
- [base64decode](base64decode.md) — decode a Base64 string
- [base64encode](base64encode.md) — Base64-encode a string
- [base64gunzip](base64gunzip.md) — decode Base64 and gunzip
- [base64gzip](base64gzip.md) — gzip-compress and Base64-encode
- [base64sha256](base64sha256.md) — SHA256 hash, Base64-encoded
- [base64sha512](base64sha512.md) — SHA512 hash, Base64-encoded
- [basename](basename.md) — last portion of a path
- [bcrypt](bcrypt.md) — Blowfish hash in Modular Crypt Format
- [can](can.md) — evaluate an expression without error
- [ceil](ceil.md) — round up to a whole number
- [chomp](chomp.md) — remove trailing newlines
- [chunklist](chunklist.md) — split a list into fixed-size chunks
- [cidrcontains](cidrcontains.md) — test whether an IP or prefix is within a CIDR prefix
- [cidrhost](cidrhost.md) — calculate a host IP within a CIDR prefix
- [cidrnetmask](cidrnetmask.md) — convert a CIDR prefix to a subnet mask
- [cidrsubnet](cidrsubnet.md) — calculate a subnet within a CIDR prefix
- [cidrsubnets](cidrsubnets.md) — calculate consecutive subnets within a CIDR prefix
- [coalesce](coalesce.md) — first non-null, non-empty argument
- [coalescelist](coalescelist.md) — first non-empty list
- [compact](compact.md) — remove empty strings from a list
- [concat](concat.md) — combine lists into one
- [contains](contains.md) — test collection membership
- [csvdecode](csvdecode.md) — decode CSV data
- [dirname](dirname.md) — remove the last portion of a path
- [distinct](distinct.md) — remove duplicate elements
- [element](element.md) — retrieve a single element by index
- [endswith](endswith.md) — test string suffix
- [ephemeralasnull](ephemeralasnull.md) — replace ephemeral values with null
- [file](file.md) — read a file as string
- [filebase64](filebase64.md) — read a file as Base64
- [filebase64sha256](filebase64sha256.md) — Base64 SHA256 of a file
- [filebase64sha512](filebase64sha512.md) — Base64 SHA512 of a file
- [fileexists](fileexists.md) — test whether a file exists
- [filemd5](filemd5.md) — MD5 of a file
- [fileset](fileset.md) — enumerate files matching a pattern
- [filesha1](filesha1.md) — SHA1 of a file
- [filesha256](filesha256.md) — SHA256 of a file
- [filesha512](filesha512.md) — SHA512 of a file
- [flatten](flatten.md) — flatten nested lists
- [floor](floor.md) — round down to a whole number
- [format](format.md) — printf-style formatting
- [formatdate](formatdate.md) — format a timestamp
- [formatlist](formatlist.md) — format values into a list of strings
- [indent](indent.md) — indent all but the first line
- [index](index.md) — find the index of a value in a list
- [issensitive](issensitive.md) — test the sensitive mark
- [join](join.md) — concatenate strings with a delimiter
- [jsondecode](jsondecode.md) — decode JSON
- [jsonencode](jsonencode.md) — encode as JSON
- [keys](keys.md) — list the keys of a map
- [length](length.md) — length of a list, map, or string
- [log](log.md) — logarithm in a given base
- [lookup](lookup.md) — look up a map element with default
- [lower](lower.md) — lowercase a string
- [matchkeys](matchkeys.md) — subset by matching indexes
- [max](max.md) — greatest number
- [md5](md5.md) — MD5 hash, hexadecimal
- [merge](merge.md) — merge maps and objects
- [min](min.md) — smallest number
- [nonsensitive](nonsensitive.md) — remove the sensitive mark
- [one](one.md) — reduce a zero-or-one-element collection
- [parseint](parseint.md) — parse an integer in a given base
- [pathexpand](pathexpand.md) — expand a leading `~` to the home directory
- [plantimestamp](plantimestamp.md) — timestamp fixed to the plan time
- [pow](pow.md) — exponentiation
- [range](range.md) — generate a list of numbers
- [regex](regex.md) — apply a regular expression
- [regexall](regexall.md) — all regular expression matches
- [replace](replace.md) — replace substring occurrences
- [reverse](reverse.md) — reverse a sequence
- [rsadecrypt](rsadecrypt.md) — decrypt an RSA ciphertext
- [sensitive](sensitive.md) — mark a value as sensitive
- [setintersection](setintersection.md) — intersection of sets
- [setproduct](setproduct.md) — Cartesian product of sets
- [setsubtract](setsubtract.md) — relative complement of sets
- [setunion](setunion.md) — union of sets
- [sha1](sha1.md) — SHA1 hash, hexadecimal
- [sha256](sha256.md) — SHA256 hash, hexadecimal
- [sha512](sha512.md) — SHA512 hash, hexadecimal
- [signum](signum.md) — sign of a number
- [slice](slice.md) — extract consecutive elements
- [sort](sort.md) — sort strings lexicographically
- [split](split.md) — split a string at a separator
- [startswith](startswith.md) — test string prefix
- [strcontains](strcontains.md) — test substring containment
- [strrev](strrev.md) — reverse a string
- [substr](substr.md) — extract a substring
- [sum](sum.md) — sum of numbers
- [templatefile](templatefile.md) — render a template file
- [templatestring](templatestring.md) — render a template string
- [textdecodebase64](textdecodebase64.md) — Base64-decode with character encoding
- [textencodebase64](textencodebase64.md) — Base64-encode with character encoding
- [timeadd](timeadd.md) — add a duration to a timestamp
- [timecmp](timecmp.md) — compare two timestamps
- [timestamp](timestamp.md) — current UTC timestamp
- [title](title.md) — uppercase the first letter of each word
- [tobool](tobool.md) — convert to boolean
- [tolist](tolist.md) — convert to list
- [tomap](tomap.md) — convert to map
- [tonumber](tonumber.md) — convert to number
- [toset](toset.md) — convert to set
- [tostring](tostring.md) — convert to string
- [transpose](transpose.md) — swap keys and values of a map of lists
- [trim](trim.md) — trim characters from both ends
- [trimprefix](trimprefix.md) — trim a prefix
- [trimspace](trimspace.md) — trim whitespace
- [trimsuffix](trimsuffix.md) — trim a suffix
- [try](try.md) — first error-free expression
- [upper](upper.md) — uppercase a string
- [urldecode](urldecode.md) — URL-decode a string
- [urlencode](urlencode.md) — URL-encode a string
- [uuid](uuid.md) — generate a UUID
- [uuidv5](uuidv5.md) — generate a name-based (version 5) UUID
- [values](values.md) — list the values of a map
- [yamldecode](yamldecode.md) — decode YAML
- [yamlencode](yamlencode.md) — encode as YAML
- [zipmap](zipmap.md) — construct a map from keys and values
