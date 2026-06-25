# api
metabook user api

## 获取API Key
打开Profile: https://metabook.ai/profile
点击用户名右侧钥匙图标，获取API Key

## 生成正文章节
你需要在Metabook创建对应作品、设定和章纲。

接口地址：
https://metabook.ai/api/v1/book/chapter/create/native

Header (以python为例）:
```
headers = {
    "Content-type": "application/json",
    "Authorization": "Bearer {}".format("你的API Key"),
}
```

POST BODY:
```
body = {
      book_uuid: "作品UUID",
      ai_service: "AI服务名称，如gemini-3-pro, gemini-3-flash, deepseek-v4-flash等等，见后面列表",
      target_chapter_number: 章节编号，integer,
      current_chapter_summary: "当前章节大纲/章纲",
      word_count: 目标字数, integer, 缺省为3000字，不超过10000
      writer_skill_id: 平台写作技能skill id, integer, 缺省为0（不用）,完整写作skill id列表见后面
      auto_save: 是否自动保存, boolean, 缺省为true
      user_prompt_id: 用户预存prompt id, integer, 非必需
      level: 后期处理, integer bitmask,  1: 快速修正, 2: 深度去AI, 4: 文风校准, 5:文风校准+快速修正,, 6: 文风校准+深度去AI, 0: 无后期处理，只要初稿
    };
```

python example:
```
import requests

url = "https://metabook.ai/api/v1/book/chapter/create/native"

body = {
      "book_uuid": "你的作品UUID",
      "ai_service": "deepseek-v4-flash",
      "target_chapter_number": 1,  # 第一章
      "current_chapter_summary": "林风和秋月被机器人打败，秋月惨死", # 章纲，不能偏离故事设定太远
      "word_count": 800,
      "writer_skill_id": 0,
      "auto_save": False,
      "user_prompt_id": 0,
      "level": 1
}

headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer "xxxxxxx",
}

response = requests.post(url, json=body, headers=headers)
print(response.json())
```

## 可用AI服务
* 注意：gemini-3-pro是指gemini 3.1 pro
* openai-5指openai 5.5
  
deepseek-v4-flash  
deepseek-v4-pro  
gemini-3-pro  
gemini-3-flash  
gemini-3-pro-jailbreak  
gemini-3-flash-jailbreak  
openai-5  
openai-mini-54  
openai-mini-52  
claude-sonnet-46  
claude-opus-46  
claude-opus-47  
claude-opus-48  
grok-4  
grok-4-fast-non-reasoning  
gemini-2.5-pro  
gemini-2.5-flash  


## 写作skill id
<img width="710" height="974" alt="image" src="https://github.com/user-attachments/assets/377281d7-21d7-4ffd-9758-7af2b7aa0eb2" />

