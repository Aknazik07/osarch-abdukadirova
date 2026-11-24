# Lab 5 - Encoding forensics

## Diagnosis (before the fix)
* file says: evidence/staff-broken.csv: Non-ISO extended-ASCII text, with CRLF line terminators (from evidence/file-before.txt)
* First 16 bytes: d2 e0 e1 2e b9 3b d4 c8 ce 3b c4 ee eb e6 ed ee (from evidence/hexdump-before.txt)

| offset | bytes | what they are |
| :--- | :--- | :--- |
| 00000000 | d2 e0 e1 2e b9 3b d4 c8 ce 3b c4 ee eb e6 ed ee | First 16 bytes of evidence/staff-broken.csv (encoded text and ; separators) |

* Encoding: Extended-ASCII / RK1048 (non-UTF-8) — evidence: evidence/file-before.txt and evidence/hexdump-before.txt
* Line ending: CRLF (0d 0a in hexdump-before.txt) — evidence: evidence/file-before.txt and evidence/hexdump-before.txt
* BOM: absent — evidence: evidence/hexdump-before.txt (starts with d2 e0, not ef bb bf)

## What each application was doing wrong
* Excel: assumed a legacy/Windows codepage instead of UTF-8 because there was no UTF-8 BOM at the start of the file, causing Cyrillic characters to display incorrectly.
* LibreOffice: misdetected or struggled with the non-standard/extended encoding and line endings when opening the raw CSV without clear UTF-8 encoding.
* cat: printed raw bytes from the terminal without converting the non-UTF-8 encoding, resulting in garbled characters.

## Fix
* Command / script: scripts/fix.sh
* Changed: encoding RK1048 / extended-ASCII -> UTF-8 with BOM; line ending CRLF -> LF; BOM added (ef bb bf) because spreadsheet/text readers (such as Excel) reliably recognize UTF-8 files when a BOM is present.

## Verification
* file after: evidence/staff-fixed.csv: Unicode text, UTF-8 (with BOM) text (from evidence/file-after.txt)
* Opened in: Excel <version>, LibreOffice Calc <version>, cat on Ubuntu <version> — evidence/opens-correctly.png
