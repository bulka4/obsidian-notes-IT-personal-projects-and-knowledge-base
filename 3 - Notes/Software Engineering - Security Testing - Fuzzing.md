Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
**Fuzzing (fuzz testing)** is a security testing technique where you send a system **large amounts of random, malformed, or unexpected inputs** to discover crashes, vulnerabilities, or incorrect behavior.

The question:
> "Can unexpected input break or compromise the system?"
# Examples
- Send invalid API requests:
```
{"user":}
{{{{{
very_long_string...
```
- Send corrupted files to a parser:
```
broken JSON
invalid image
malformed PDF
```
- Send unusual values:
```
negative numbers
huge numbers
empty strings
special characters
```

It looks for:
- crashes
- memory errors
- security vulnerabilities
- unexpected behavior

Example:
```
Fuzzer generates input
        ↓
Application processes it
        ↓
Application crashes ❌
        ↓
Bug found
```

Fuzzing is related to **input validation testing** and **property-based testing**, but in security it is mainly used to discover weaknesses by attacking the system with unexpected inputs.