---
title: Snakemake benchmark summarizing
description: With a simple perl script
published: true
date: 2020-04-15T02:07:17.681Z
tags: script, tips, snakemake, bioinfo
---

# Usage

```bash
❯ workflow/scripts/sum_benchmark.pl
Total Execution time: 10 hours 04 minutes 44 seconds
```

> This script will find file(s) which name match `*.benchmark` for time summarize.

# Source

```perl
#!/usr/bin/perl
use strict;
use warnings;

my $total_sec;
my $files=`find . -name "*.benchmark"`;
chomp($files);
# print "$files\n";
my @lines=split(/\n/,$files);
foreach my $file (@lines) {
	open(IN,$file);
	while (<IN>) {
		if ($_ !~ /^s/) {
			my @arr=split/\t/;
			$total_sec+=$arr[0];
		}
	}
	close IN;
}
printf ("Total Execution time: %02d hours %02d minutes %02d seconds\n",(gmtime($total_sec))[2,1,0]);
```