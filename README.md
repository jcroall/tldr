# What is TLDR?

TLDR is a popular internet acronym for "Too Long; Didn't Read". It's accepted usage prefixes a summary of a longer body of text.
TLDR for Black Duck summarizes Black Duck log packages and gives you the summary of the issues, so you don't need to scroll through massive log files.
TLDR will also work on Coverity log files if you add the flag `--isCoverity true`, although it is designed for Black Duck

## How do I install it?

Make sure to install the requirements.txt file: `pip3 install -r requirements.txt`

## How does it work?

Using Python3, there are several different search modes that TLDR can be run as to ensure that you are parsing out the data you need. By default it will attempt to unzip the small zip package from the logs, but you can specify the standard.zip by setting the property `--size STANDARD`

TLDR will create a tldr directory named after your log package that will collect your results from the individual scans that it runs. These are summaries built from the errors that happened in the logs. You most likely still need to reference the original log package for the full picture, but this will help draw your attention to the problems happening within the logs.

Summarize - this feature is enabled by default, and will parse out all WARNs, ERRORs, Stack Traces, and Exceptions from the logs. This feature can be disabled by passing the following flag at run time: `--skip-summary TRUE`

String Search - this feature is enabled when passing the flag `--string <Desired String Here>`, it will perform a basic search against the logs looking for all lines containing your desired string.

Scan ID - passing the flag `--scanid <scanID>` will perform a search on the passed scan ID. It will inform you the first log file/line it encountered the scan ID, and the last file to have that scan ID, as well as printing all lines containing that ID.

Fuzzy Search - Fuzzy Searching can be enabled by using the flag --fuzzy-search "Word or Phrase here". It can be used with phrases, as well as individual words, and will find similar words/phrases within a specific similarity threshold, and if the word/line qualifies, it will write the line to a fuzzySearch.log file

Keyword searching - This feature gets enabled with the flag `--keywords "one,two,three"`. You can pass a coma separated list of keywords to basic search for, and it will create a keywords.log file containing every line that contains any of your keywords.

Detect timeout recommendation - TLDR will also analyze the lengths of completed scans according to the passed log package, and will suggest a Detect timeout window to allow for 99% success with your Detect scans.

Suspect API calls - Checks the nginx access logs for calls with a `limit` query parameter > 300

It also will automatically fetch sysinfo, jobinfo, scaninfo, and if it exists in the log package, the system check.

## Usage

`python3 tldr.py --log blackducklogs.zip --size small --string "ScanPurgeJob" --fuzzy-search "dispatch" --keywords "ScanAutoBomJob,VersionBomComputationJob" --scanid "9535e51d-7955-4a26-8e54-bc02a92453fd" --skip-summary TRUE`
