# Data hunting (Bandit 11, 12, 13, 14, 15, 16)


## The concept
Between the levels 11 and 16, I learned about how hard it can be to find the information you are looking for, if you don't know the right commands. There are two ways of hidding text information: by transformation and by layers. Both of them work to hide information, not to prevent others from finding it, because the information is just in a different form, but not inaccessible. 

## How it works
When an information is hidden by transformation, it is encoded, so it is necessary to use specific commands to decode it. It can be done, for example, with base64, ROT13 or hex, all of them work. When the information is hidden by layers, it is compressed multiple times, what makes it harder to find the information, but using the right commands, it is a question of time to find it. When the base64 was used, the command you need to use is "base64 -d", that makes the information that was encoded be in its normal way again. On the other hand, when it is encoded by ROT13, you need to use the command "tr 'A-Za-z' 'N-ZA-Mn-za-m'", in order to decode it again. If the information is compressed, it can be in some formats, such as gzip, bzip2 and tar, and to decompress it, the right command is "gzip -d FILE" when the file is compressed by gzip, "bzip2 -d FILE" when it is compressed by bzip2 and "tar xf FILE" when it is decompressed by tar. Before doing anything of that, it is necessary to identify which type of compression it is, using "file", and only then start the process with the right command.

## The diagnostic path
As I said in the end of the "How it works" paragraph, you can't just start using all the commands just because you know them, first, you need to identify which type of compression or decoding you're dealing with, using "file". That needs to be done every time the file changes its format, because after every decoding , it changes, and you will probably need to use a different command.

## Real-world relevance
All this is really important in real work, because you can analyze obfuscated data, do a forensics work or find malware that is hidden in the system by encoding layers. Encoding is part of the basics about prompt injection, because it works as decoded input that passes through naive filters.

## Key commands
- `bzip2 -d` - decompress files in bzip2 format
- `gzip -d` - decompress files in gzip format
- `tar xf` - extract files from a tar archive
- `file` - shows the format of the file
- `base64 -d` - decode files in base64 format
- `tr 'A-Za-z' 'N-ZA-Mn-za-m'` - decode files in ROT13 format