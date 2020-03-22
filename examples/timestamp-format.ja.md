# Timestamp format

Contents:

* [Summary](#summary)
  * [Issue](#issue)
  * [Decision](#decision)
  * [Status](#status)
* [Details](#details)
  * [Assumptions](#assumptions)
  * [Constraints](#constraints)
  * [Positions](#positions)
  * [Argument](#argument)
  * [Implications](#implications)
* [Related](#related)
  * [Related decisions](#related-decisions)
  * [Related requirements](#related-requirements)
  * [Related artifacts](#related-artifacts)
  * [Related principles](#related-principles)
* [Notes](#notes)


## 概要


### 課題

タイムスタンプを使って
We want to be able to track when things happen by using timestamps and by using a consistent timestamp format that works well across all our systems and third-party systems.

We interact with systems that have different timestamp formats:

* JSON messages do not have a native timestamp format, so we need to choose how to convert a timestamp to a string, and convert a string to a timestamp, i.e. how to serialize/deserialize.

* Some applications are set to use local time, rather than UTC time. This can be convenient for projects that must adjust to local time, such as projects that trigger events that are based on local time.

* Some systems have different time precision needs and capabilities, such as using a time resolution of seconds vs. milliseconds vs. nanoseconds. For example, the Linux operating system `date` command uses a default time precision of seconds, whereas the Nasdaq stock exchange wants a default time precision of nanoseconds.


### Decision

We choose the timestamp standard format ISO 8601 with nanosecond precision, specifically "YYYY-MM-DDTHH:MM:SS.NNNNNNNNNZ".

The format shows the year, month, day, hour, minute, second, nanoseconds, and Zulu time zone a.k.a. UTC, GMT.


### Status

Decided.


## Details


### Assumptions

私たちはこれらのタイムスタンプの文字列を扱い、タイムスタンプ型から文字列へ変換(シリアライズ)したり、文字列からタイムスタンプ型へ変換(デシリアライズ)したりする必要がある。

そのフォーマットは使いやすく、変換しやすく、人が読めるものであることが望ましい。

分析システムやデータベース、金融システムなど、私たちのコントロールできない外部システムと互換性があるようにしたい。


### 制約

いくつかのシステムは、時間の精度に制限がある。例えばMacOSの `date` コマンドは、秒までの精度でしか表示でず、ナノ秒を扱えない。

### Positions

以下の選択肢を検討した。

* Unixエポック、つまり単調増加する数値

* 簡潔なテキストフォーマット "YYYYMMDDTHHMMSSNNNNNNNNN"

* ローカルタイムゾーンとUTCタイムゾーンを使う。

### 議論


For typical use, we value easy to read/write by humans, more than raw speed/size.

For typical use, we want a format that works fine in machine systems, and also works well manually, such as writing sample data, reading JSON output, grepping a log file, etc.

For atypical use, such as high performance computing, we expect we'll want to optimize any text format we choose by converting the text to a faster format, such as a programming language's built-in date object type. So the text format doesn't matter much for HPC.


### 考察

私たちの様々なテキストシステムと時間のシステムは、このフォーマットで合致させなければならない。

## Related

### Related decisions

期間(duration)のようにある時間の差を扱う速く/簡単な方法が必要なこともある。これらは、UNIXエポックのタイムスタンプで扱うのが簡単だ。

### Related requirements

Splunk, Sumo, ELKなどのログメッセージの種類に関した要求があれば、私たちの決定を調整する必要があるかもしれない。

### Related artifacts

Language formatters and parsers:

  * [date-fns: Modern JavaScript date utility library](https://date-fns.org/)
  * [Crono: date and time library for Rust](https://github.com/chronotope/chron)
  
Rosetta Codeの例:

  * [System time](https://www.rosettacode.org/wiki/System_time)
  * [Data format](https://www.rosettacode.org/wiki/Date_format)
  * [Show the epoch](https://www.rosettacode.org/wiki/Show_the_epoch)

SixArm examples:

  * [now_string](https://github.com/SixArm/rosetta_code/tree/master/tasks/now_string)


### Related principles

Easily reversible. We can change pretty easily to a different format, such as Unix epoch.

Defer premature optimization. For typical use we don't care much about a handful of extra characters such as a format that uses dashes and colons.


## Notes

Add notes here.
