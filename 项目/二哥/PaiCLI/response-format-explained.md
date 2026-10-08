# response_format 详解

## 什么是 response_format？

**response_format** 是 LLM API 请求中的一个**参数**，用于告诉 API："我要求你返回的内容必须是某种特定格式"。

---

## 类比理解

想象你在餐厅点餐：

### 没有 response_format
```
你: "给我做个汉堡"
厨师: "好的" 
      → 可能给你牛肉汉堡
      → 可能给你鸡肉汉堡
      → 可能还附带薯条
      → 完全由厨师决定
```

### 有 response_format
```
你: "给我做个汉堡，必须按照这个配方：
     - 面包：芝麻面包
     - 肉饼：牛肉
     - 配菜：生菜、番茄
     - 不要薯条"
     
厨师: "明白，严格按配方做"
      → 保证输出符合你的要求
```

---

## 技术层面的解释

### 普通 API 调用（无格式约束）

```json
// 请求
{
  "model": "glm-5.1",
  "messages": [
    {"role": "user", "content": "分析这段代码的复杂度"}
  ]
}

// 可能的响应1（自然语言）
"这段代码的复杂度是中等的，因为..."

// 可能的响应2（非标准JSON）
"代码分析结果：
 - 复杂度: 中等
 - 建议: ..."

// 可能的响应3（JSON但不规范）
```json
{
  "result": "中等复杂度",
  "extra_info": "..."
}
```
```

**问题**：返回格式不可控，每次可能不一样，难以解析。

---

### 带 response_format 的调用（格式约束）

```json
// 请求
{
  "model": "glm-5.1",
  "messages": [
    {"role": "user", "content": "分析这段代码的复杂度"}
  ],
  "response_format": {
    "type": "json_schema",
    "json_schema": {
      "name": "code_analysis",
      "schema": {
        "type": "object",
        "properties": {
          "complexity": {"type": "string", "enum": ["low", "medium", "high"]},
          "score": {"type": "number"},
          "issues": {"type": "array"}
        },
        "required": ["complexity", "score"]
      }
    }
  }
}

// 保证的响应（严格符合 Schema）
{
  "complexity": "medium",
  "score": 65,
  "issues": ["嵌套过深", "缺少注释"]
}
```

**好处**：
- ✅ 格式固定，易于解析
- ✅ 字段类型保证（不会把数字返回成字符串）
- ✅ 必填字段保证存在
- ✅ 可以直接反序列化为 Java 对象

---

## response_format 的两种模式

### 模式1：json_object（宽松模式）

```json
{
  "response_format": {
    "type": "json_object"
  }
}
```

**作用**：只保证返回的是**合法的JSON**，但不约束具体结构。

**示例**：
```json
// 可能返回
{"result": "success", "data": {...}}

// 也可能返回
{"answer": "...", "code": 200}

// 只要是合法JSON即可
```

### 模式2：json_schema（严格模式）

```json
{
  "response_format": {
    "type": "json_schema",
    "json_schema": {
      "name": "response",
      "schema": {
        "type": "object",
        "properties": {
          "result": {"type": "string"}
        },
        "required": ["result"]
      }
    }
  }
}
```

**作用**：不仅保证是JSON，还保证**字段名、类型、必填项**都符合要求。

---

## 为什么需要 API 原生支持？

### 方式1：API 原生支持（推荐）

```
你发送请求 + response_format
        ↓
API 内部机制保证输出格式
        ↓
100% 返回符合要求的 JSON
```

**优点**：
- ✅ 可靠性高（API底层保证）
- ✅ 不需要重试
- ✅ 性能好

### 方式2：Prompt 约束（备用）

```
你在 Prompt 中说："请按JSON格式输出"
        ↓
LLM 尝试理解你的要求
        ↓
可能返回正确格式，也可能不是
        ↓
需要验证 + 重试
```

**缺点**：
- ⚠️ 不保证100%符合
- ⚠️ 可能需要多次重试
- ⚠️ 浪费 Token

---

## GLM API 是否支持 response_format？

### 需要验证的方法

#### 方法1：查看官方文档

```bash
# 查看 GLM API 文档
https://open.bigmodel.cn/dev/api
```

#### 方法2：实际测试

```java
// 发送带 response_format 的请求
ObjectNode requestBody = mapper.createObjectNode();
requestBody.put("model", "glm-5.1");
// ...

ObjectNode responseFormat = requestBody.putObject("response_format");
responseFormat.put("type", "json_object");

// 发送请求，看是否报错
```

**可能的结果**：
1. ✅ **支持** → 正常返回JSON
2. ❌ **不支持** → 返回错误："unknown parameter: response_format"
3. ⚠️ **忽略** → 不报错但不生效

---

## 如果 GLM 不支持怎么办？

### 替代方案对比

| 方案 | 实现难度 | 可靠性 | 适用场景 |
|------|---------|-------|---------|
| **Prompt Engineering** | ⭐ 简单 | ⭐⭐ 60-80% | 简单结构 |
| **Prompt + 重试** | ⭐⭐ 中等 | ⭐⭐⭐ 80-95% | 通用 |
| **工具调用模拟** | ⭐⭐⭐ 复杂 | ⭐⭐⭐⭐ 95%+ | 结构化输出 |
| **后处理修复** | ⭐⭐ 中等 | ⭐⭐⭐ 85%+ | 可容错场景 |

### 实际推荐方案

```java
public ChatResponse chatWithStructuredOutput(
    List<Message> messages, 
    JsonSchema schema
) throws IOException {
    
    // 1. 在 System Prompt 中强调格式
    String formatInstruction = """
        你必须严格按照以下JSON Schema输出，不要有任何额外文字：
        
        %s
        
        重要规则：
        - 只返回JSON，不要用markdown代码块包裹
        - 不要添加任何解释说明
        - 确保所有必填字段都存在
        """.formatted(schema.schema().toPrettyString());
    
    List<Message> augmentedMessages = new ArrayList<>();
    augmentedMessages.add(Message.system(formatInstruction));
    augmentedMessages.addAll(messages);
    
    // 2. 最多重试3次
    for (int attempt = 0; attempt < 3; attempt++) {
        ChatResponse response = chat(augmentedMessages, null);
        String content = cleanJsonOutput(response.content());
        
        // 3. 验证输出
        try {
            JsonNode json = mapper.readTree(content);
            if (validateSchema(json, schema)) {
                return new ChatResponse(
                    response.role(), 
                    content, 
                    null, 
                    response.inputTokens(), 
                    response.outputTokens()
                );
            }
        } catch (Exception e) {
            // JSON解析失败，重试
        }
        
        // 如果失败，在下次请求中加入反馈
        augmentedMessages.add(Message.assistant(content));
        augmentedMessages.add(Message.user(
            "输出格式不正确，请严格按照Schema再试一次"
        ));
    }
    
    throw new IOException("无法获得符合格式的输出");
}

private String cleanJsonOutput(String content) {
    return content
        .replaceAll("^```json\\s*", "")
        .replaceAll("^```\\s*", "")
        .replaceAll("```\\s*$", "")
        .trim();
}
```

---

## 实际使用建议

### 1. 先测试 API 是否支持

```java
// 简单测试
try {
    ObjectNode req = mapper.createObjectNode();
    req.put("model", "glm-5.1");
    req.putArray("messages")
       .addObject()
       .put("role", "user")
       .put("content", "返回JSON: {\"test\": true}");
    
    req.putObject("response_format")
       .put("type", "json_object");
    
    // 发送请求
    // 如果成功 → 支持
    // 如果报错 → 不支持
} catch (Exception e) {
    System.out.println("不支持 response_format");
}
```

### 2. 根据测试结果选择方案

```java
public class StructuredOutputClient {
    private final boolean supportsResponseFormat;
    
    public StructuredOutputClient(String apiKey) {
        this.supportsResponseFormat = testResponseFormatSupport();
    }
    
    public ChatResponse getStructuredOutput(
        List<Message> messages,
        JsonSchema schema
    ) throws IOException {
        if (supportsResponseFormat) {
            return chatWithNativeFormat(messages, schema);
        } else {
            return chatWithPromptEngineering(messages, schema);
        }
    }
}
```

---

## 总结

### response_format 是什么？
一个 API 请求参数，用于约束 LLM 输出格式。

### 为什么重要？
- 保证输出可解析
- 减少错误处理
- 提高程序可靠性

### 怎么用？
1. 如果 API 支持 → 直接在请求中添加
2. 如果不支持 → 用 Prompt + 验证 + 重试

### 类似的功能
- OpenAI: ✅ 支持 `response_format`
- Anthropic Claude: ✅ 支持 (通过 tool use)
- Google Gemini: ✅ 支持 `response_mime_type`
- GLM: ❓ 需要查文档或测试
