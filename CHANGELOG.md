# Dataset versions

## v1.1 - 20 October 2026

Final submission version. Exports explicitly use LF line endings for reproducibility
across operating systems; checksum metadata is recomputed from these exact files.
CSV line endings are protected from Git conversion with .gitattributes.
No records, column definitions or analytical values changed from v1.0.

## v1.0 - 20 October 2026

Initial publication. Git normalized CSV line endings, making the original checksum
metadata inconsistent with the public downloads. The original tag is preserved.
Use v1.1, whose public downloads have been checked byte-for-byte.
