Tags: [[__Infrastructure_Engineering]] [[_Linux & Bash]]
#InfrastructureEngineering #LinuxBash 

# Introduction
For editing files the best tools are:
- `sed` - More information in the ‘Sed’ section of this document.
- `cat` used together with heredoc and command redirection - More information in the ‘Heredoc’ section of this document.
## Sed
Sed is used to replace all the strings matching the pattern with a new string in a specific file:
- `sed -i ‘s/pattern/replacement/’ file_path`

Patterns which are being matched to strings are using Regular Expressions, more information is here: [link](https://www.gnu.org/software/sed/manual/html_node/Regular-Expressions.html).
## Heredoc
Heredoc is used in order to pass a multiline argument to a command:
```bash
Command << EOF
Line1
Line2
EOF
```

For example it can pass a multiline text as an argument to the Cat command what will display all those lines.

If we additionally use the ‘>’ or ‘>>’ to redirect an output we can save multiline text to a file:
```bash
Cat << EOF >> file_path
Line1
Line2
EOF
```