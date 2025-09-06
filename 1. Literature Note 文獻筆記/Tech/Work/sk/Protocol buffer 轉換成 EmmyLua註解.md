---
tags: 
date: 2024-05-09
time: 14:39
---
[chatgpt](https://chat.openai.com/share/382bea00-56ca-43bf-add1-d1c48a12ccf3)

```python
import re

def protobuf_to_emmylua(proto_file):
    emmylua_content = []

    # 讀取 Protocol Buffer 文件
    with open(proto_file, "r") as f:
        lines = f.readlines()

    # 解析每行並生成 EmmyLua 註解
    for line in lines:
        line = line.strip()
        if line.startswith("message"):
            message_name = line.split(" ")[1]
            emmylua_content.append(f"---@class {message_name}\n")
        elif line.startswith("\trequired") or line.startswith("\toptional") or line.startswith("\trepeated"):
            parts = line.split()
            field_type = parts[1]
            field_name = parts[2].split("=")[0]
            # 將 Protocol Buffer 的類型轉換為對應的 EmmyLua 類型
            field_type = re.sub(r"int32|int64|uint32|uint64|sint32|sint64|fixed32|fixed64|sfixed32|sfixed64", "number", field_type)
            field_type = re.sub(r"string|bytes", "string", field_type)
			field_type = re.sub(r"bool", "boolean", field_type)

            emmylua_content.append(f"---@field {field_name} {field_type}\n")

    # 將生成的 EmmyLua 註解寫入文件
    emmylua_file = os.path.splitext(proto_file)[0] + ".lua"
    with open(emmylua_file, "w") as f:
        f.writelines(emmylua_content)

    print(f"成功將 {proto_file} 轉換為 EmmyLua 格式：{emmylua_file}")

# 執行轉換
protobuf_to_emmylua("your_protobuf.proto")

```


[[2024-09-20|2024-09-20, 17:39]]
因為忘記我把腳本存在這了，這次用copilot 生成腳本。

```python
import re
import sys
  
def parse_proto_file(proto_file):
	with open(proto_file, 'r') as file:
	lines = file.readlines()
	messages = {}
	current_message = None
  
for line in lines:

line = line.strip()

if line.startswith('message'):

current_message = line.split()[1]

messages[current_message] = []

elif current_message and line.startswith('}'):

current_message = None

elif current_message:

match = re.match(r'(optional|repeated)?\s*(\w+)\s+(\w+)\s*=\s*\d+;', line)

if match:

field_modifier, field_type, field_name = match.groups()

if field_type in ['int32', 'int64', 'sint32', 'sint64']:

field_type = 'number'

elif field_type == 'bool':

field_type = 'boolean'

if field_modifier == 'repeated':

field_type += '[]'

messages[current_message].append((field_type, field_name))

return messages

  

def generate_emmylua_comments(messages):

comments = []

for message, fields in messages.items():

comments.append(f'---@class {message}')

for field_type, field_name in fields:

comments.append(f'---@field {field_name} {field_type}')

comments.append('')

return comments

  

def write_emmylua_file(comments, output_file):

with open(output_file, 'w') as file:

for comment in comments:

file.write(comment + '\n')

  

def main():

if len(sys.argv) != 3:

print("Usage: python script.py <input_proto_file> <output_lua_file>")

sys.exit(1)

proto_file = sys.argv[1]

output_file = sys.argv[2]

messages = parse_proto_file(proto_file)

comments = generate_emmylua_comments(messages)

write_emmylua_file(comments, output_file)

  

if __name__ == '__main__':

main()
```