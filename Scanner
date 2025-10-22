import re
import sys

# C keywords list
keywords = {
    "int", "float", "if", "else", "while", "for", "return", "void", "char",
    "double", "switch", "case", "default", "break", "continue", "struct",
    "union", "enum", "typedef", "const", "sizeof", "long", "short", "signed",
    "unsigned", "static", "extern", "register", "volatile"
}

# Token type enumeration
class TokenType:
    KEYWORD = "Keyword"
    IDENTIFIER = "Identifier"
    OPERATOR = "Operator"
    NUMERIC_CONSTANT = "Numeric_Constant"
    CHARACTER_CONSTANT = "Character_Constant"
    SPECIAL_CHARACTER = "Special_Character"
    COMMENT = "Comment"
    WHITESPACE = "Whitespace"
    NEWLINE = "Newline"

# Token class to store type and value
class Token:
    def __init__(self, token_type, value):
        self.type = token_type
        self.value = value

    def __str__(self):
        return f"{self.type}: {self.value}"

# Scanner function
def scanner(code):
    tokens = []
    # Regular expressions for C tokens
    token_specification = [
        (TokenType.COMMENT, r'//.*?$|/\*.*?\*/', re.DOTALL | re.MULTILINE),  
        (TokenType.KEYWORD, r'\b(?:' + '|'.join(keywords) + r')\b'),
        (TokenType.IDENTIFIER, r'[a-zA-Z_]\w*'),
        (TokenType.OPERATOR, r'[+\-*/%=&|!<>]+'),
        (TokenType.NUMERIC_CONSTANT, r'\b\d+(\.\d+)?([eE][+-]?\d+)?\b'),
        (TokenType.CHARACTER_CONSTANT, r"\'(\\.|[^\\'])\'"),
        (TokenType.SPECIAL_CHARACTER, r'[.,;()\[\]{}]'),
        (TokenType.WHITESPACE, r'[ \t]+'),
        (TokenType.NEWLINE, r'\n')
    ]
    token_regex = '|'.join(f'(?P<{pair[0]}>{pair[1]})' for pair in token_specification)
    comment_flags = re.DOTALL | re.MULTILINE

    # Tokenizing code
    for match in re.finditer(token_regex, code, flags=comment_flags):
        token_type = match.lastgroup
        value = match.group(token_type)
        tokens.append(Token(token_type, value))

    return tokens

print("Enter a C code then press Ctrl+D (2 times) (linux/mac) or Ctrl+z (2 times) (windows): ")
code = sys.stdin.read();
tokens = scanner(code)
print("\n=========================================SCANNER=============================================")
for token in tokens:
    print(token)
