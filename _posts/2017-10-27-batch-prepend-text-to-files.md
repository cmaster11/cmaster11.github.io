---
title: Batch prepend text to files
---

Easy way to prepend some text to a group of files in a directory and subdirectories:

```
# Text to prepend
PREPEND_TEXT="import {h} from 'preact';"

# Searches for .tsx files
find . -name '*.tsx' -print0 | 
while IFS= read -rd '' file; 
do 
	# Outputs to abc.tsx.new
	# Flag -e is used to be able to append also \n
	# See: https://linux.die.net/man/1/echo
	echo -e "$PREPEND_TEXT" | cat - $file > "$file.new";
	# Replaces old abc.tsx with the new one
	mv "$file.new" $file; 
done
```