```python
import json  
  
import allure  
import requests  
  
BASE_URL = "https://open.bigmodel.cn/api/paas/v4/chat/completions"  
MODEL = "glm-4.7"  
  
  
def _headers():  
    api_key = "e8f3120bc0ae457da83952ba121af892.g5hXB2Xlros9sdBp"  
    if not api_key:  
        raise RuntimeError("请先设置环境变量 BIGMODEL_API_KEY")  
    return {  
        "Authorization": f"Bearer {api_key}",  
        "Content-Type": "application/json",  
    }  
  
  
@allure.feature("大模型接口")  
@allure.story("Chat Completions")  
@allure.title("正常对话：输入“你好”应返回 assistant 内容")  
@allure.tag("smoke", "glm")  
@allure.severity(allure.severity_level.CRITICAL)  
def test_chat_hello():  
    payload = {  
        "model": MODEL,  
        "messages": [  
            {"role": "user", "content": "你好"}  
        ]  
    }  
    with allure.step("发送 chat/completions 请求"):  
        resp = requests.post(BASE_URL, headers=_headers(), json=payload, timeout=30)  
  
        allure.attach(  
            json.dumps(payload, ensure_ascii=False, indent=2),  
            name="请求体 payload",  
            attachment_type=allure.attachment_type.JSON,  
        )  
        allure.attach(  
            f"status_code={resp.status_code}\n\n{resp.text}",  
            name="响应原文",  
            attachment_type=allure.attachment_type.TEXT,  
        )  
  
    with allure.step("校验 HTTP 状态码为 200"):  
        assert resp.status_code == 200  
  
    with allure.step("校验响应结构包含 choices[0].message.content"):  
        data = resp.json()  
        # 下面这些字段名以 OpenAI 风格为参考；如果你的实际返回不同，跑一次看 resp.text 再改断言  
        assert "choices" in data and len(data["choices"]) > 0  
        assert "message" in data["choices"][0]  
        assert "content" in data["choices"][0]["message"]  
  
        content = data["choices"][0]["message"]["content"]  
        allure.attach(  
            content,  
            name="模型输出 content",  
            attachment_type=allure.attachment_type.TEXT,  
        )  
        assert isinstance(content, str) and len(content.strip()) > 0
```

```bash
pytest .\study\allure_study.py --alluredir=allure-results --clean-alluredir
```
`--alluredir=./allure-results` == 👉 **告诉 pytest：  把“测试执行过程中产生的 Allure 原始数据”保存到这个目录里。**

```bash
allure serve ./allure-results
```
把测试结果转换为**HTML 报告**
